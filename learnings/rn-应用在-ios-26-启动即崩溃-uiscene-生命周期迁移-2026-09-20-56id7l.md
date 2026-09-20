---
title: "RN 应用在 iOS 26+ 启动即崩溃：UIScene 生命周期迁移"
author: foxi-ui
date: 2026-09-20
tags: [react-native, ios, troubleshooting, uiscene, xcode]
---

## 背景

React Native 0.87.1 项目在 iOS 27 模拟器上执行 `yarn ios`：构建成功、安装成功、CLI 明确打印
`success Successfully launched the app`，但 App 启动后不到 1 秒即退回桌面，进程消失，且没有任何
JS 层日志。

这个问题的暴露过程本身也有价值：它被 **4 层 Xcode 环境问题**挡在后面 —— `xcode-select` 指向
CommandLineTools、Xcode 许可协议未接受、CoreSimulator 缺失、iOS 模拟器运行时未下载。每修好一层
才露出下一层，很容易误判为"同一个问题反复修不好"。

## 定位过程

1. **不要相信 CLI 的 success**。`react-native run-ios` 的 "Successfully launched the app" 只表示
   `simctl launch` 这个调用没报错，**不代表进程活着**。
2. 用 `ps` 精确匹配 app 二进制路径确认进程存活：
   `ps aux | grep "<App>.app/<App>" | grep -v grep`
   注意**别用项目名 grep** —— 会误匹配到 Metro 的 node 进程（其命令行含项目路径），得到假阳性。
3. 更可靠的判定：`xcrun simctl io booted screenshot /tmp/sim.png` 截图看实际画面。主屏幕 vs App
   界面一目了然，且截图体积会差一个数量级（主屏幕约 3.8MB，纯色 App 界面约 300KB）。
4. iOS 崩溃报告在 **`~/Library/Logs/DiagnosticReports/<AppName>-<时间>.ips`**，
   **不在**模拟器内部的 DiagnosticReports 目录（那里通常不存在）。
5. 解析 `.ips`：文件是「第 1 行 JSON header + 其余为 JSON body」，用 python 按首个换行切片即可：

   ```python
   raw = open(path).read(); i = raw.index('\n')
   hdr, body = json.loads(raw[:i]), json.loads(raw[i:])
   ```

   取崩溃线程（`threads[].triggered == True`）的 `frames[]`，配合 `usedImages[]` 还原符号。

6. 得到的调用栈直接给出了根因，无需再猜：

   ```
   exception: EXC_BREAKPOINT / SIGTRAP  ("Trace/BPT trap: 5")
   UIKitCore  ___UIApplicationEvaluateRuntimeIssueForNoSceneLifecycleAdoption_block_invoke
   ```

## 根因

Apple 从 iOS 18.4 起只打日志警告：

> This process does not adopt UIScene lifecycle. This will become an assert in a future version.

到 **iOS 26/27 变成硬崩溃**。触发条件是二者同时满足：

1. App 以 iOS 26+ SDK 编译
2. `Info.plist` 缺少 `UIApplicationSceneManifest`

RN 0.87.1 的官方模板仍是旧的 window-based 生命周期（`AppDelegate` 里直接
`UIWindow(frame: UIScreen.main.bounds)` 并调 `startReactNative`），因此新 SDK 上默认生成的项目必然
启动即崩。这是**框架模板滞后于 SDK**，不是项目配置写错。

## 解决方案

两处改动，**不新建文件**。

### 1. `Info.plist` 增加 scene manifest

```xml
<key>UIApplicationSceneManifest</key>
<dict>
	<key>UIApplicationSupportsMultipleScenes</key>
	<false/>
	<key>UISceneConfigurations</key>
	<dict>
		<key>UIWindowSceneSessionRoleApplication</key>
		<array>
			<dict>
				<key>UISceneConfigurationName</key>
				<string>Default Configuration</string>
				<key>UISceneDelegateClassName</key>
				<string>$(PRODUCT_MODULE_NAME).SceneDelegate</string>
			</dict>
		</array>
	</dict>
</dict>
```

用 `plutil -lint` 校验，`plutil -extract UIApplicationSceneManifest xml1 -o -` 复查读取结果。

### 2. 在 `AppDelegate.swift` 内新增 `SceneDelegate`（同一文件）

`AppDelegate` 保留 factory 初始化，但不再自建 window：

```swift
class SceneDelegate: UIResponder, UIWindowSceneDelegate {
  var window: UIWindow?

  func scene(_ scene: UIScene,
             willConnectTo session: UISceneSession,
             options connectionOptions: UIScene.ConnectionOptions) {
    guard let windowScene = scene as? UIWindowScene,
          let appDelegate = UIApplication.shared.delegate as? AppDelegate,
          let factory = appDelegate.reactNativeFactory
    else { return }

    let window = UIWindow(windowScene: windowScene)
    self.window = window
    appDelegate.window = window

    factory.startReactNative(withModuleName: "AppName",
                             in: window,
                             launchOptions: nil)
  }
}
```

**关键点**：RN 的 `RCTReactNativeFactory` 只提供 `startReactNativeWithModuleName:inWindow:launchOptions:`，
**没有 scene 专用 API，也不需要**。它内部只是 `window.rootViewController = rootViewController` +
`makeKeyAndVisible`，所以从 Scene 侧把基于 `windowScene` 创建的 window 传进去即可。

`$(PRODUCT_MODULE_NAME)` 会解析为 target 名（未显式设置时取 `PRODUCT_NAME`），即
`AppName.SceneDelegate`。

## 经验总结

- **`react-native run-ios` 报 success ≠ App 能跑**。验收必须看进程是否存活 + 截图，不能只看 CLI
  输出。这类"构建链路全绿但运行时崩溃"的问题，只靠 CLI 日志会完全看不见。
- **新增 `.swift` 文件会把改动扩散到 `project.pbxproj`**（要手工补 `PBXBuildFile`、
  `PBXFileReference`、`Sources` build phase 三个条目，易出错）。**把新类写在已有文件内可以完全绕开
  pbxproj 改动**，是这类场景更稳的做法。
- `.ips` 崩溃报告是「首行 JSON header + 其余 JSON body」的拼接格式，不是单个合法 JSON，直接
  `json.load` 会失败。
- 遇到 `UIKitCore` 里形如 `...EvaluateRuntimeIssue...` 的符号，基本可以直接判定为 **SDK 的强制要求**
  （Apple 把"未来会 assert"的警告正式升级成了断言），优先按"必须迁移"处理，而不是找绕过开关。
- 环境问题的排查顺序：`xcode-select -p` → `xcodebuild -version` → `xcrun simctl list runtimes` →
  `xcrun simctl list devices available`。四步能覆盖绝大部分 iOS 构建环境的初始化缺失。
- **迁移副作用（务必检查）**：scene 生命周期下，首启 deep link 参数从 `didFinishLaunchingWithOptions`
  的 `launchOptions` 变为 `connectionOptions`，`Linking.getInitialURL()` 会返回 `nil`。需要从
  `connectionOptions.urlContexts` 转发。未使用 Linking 的项目无影响；已使用的项目迁移时必须一并处理。

## 相关 Skills

- troubleshooting
- bug-fix
- superpowers:systematic-debugging
