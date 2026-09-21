---
title: "RN iOS 启动即崩 'Global was not installed'：加了原生依赖却没跑 pod install"
author: foxi-ui
date: 2026-09-21
tags: [react-native, ios, cocoapods, troubleshooting, react-navigation, debugging]
---

## 背景

React Native 0.87.1 裸工程（新架构 Fabric/bridgeless），为接入导航 `yarn add` 了
`@react-navigation/native`、`@react-navigation/native-stack`（连带 `react-native-screens` 4.28.0）。

之后 `yarn ios`：**构建成功、安装成功、CLI 明确打印 `success Successfully launched the app`**，
但 App 起来就崩：

```text
[runtime not ready]: Error: Non-js exception:
AppRegistryBinding::startSurface failed. Global was not installed.
```

## 定位过程

### 阶段性错误：把「重建」当成解法

第一反应是「加了原生依赖，需要重建」。于是重建了一次 —— 编译成功、`.app` 时间戳更新到崩溃前
一分钟，**崩溃照旧**。

这个失败很有价值：它说明问题不在「编不编」，而在「编什么」。**重建只重编 JS 侧和已有的原生代码；
缺的原生代码不会因为重建而出现。**

### 有效证据：比对依赖与锁文件的时间戳

拆开看两个时间：

| 文件 | 状态 |
|---|---|
| `package.json` / `yarn.lock` | 已含新依赖 |
| `ios/Podfile.lock` | 停留在加依赖**之前** |

```bash
grep -c RNScreens ios/Podfile.lock   # → 0
```

原生 pod 从未安装。判据成立。

### 无效证据：拿 Pods 目录结构当判据（我踩的坑）

同一轮我还查过 `ls ios/Pods/RNScreens` → 不存在，并据此佐证「pod install 没跑过」。
**结论碰巧对了，但推理是错的：**

`Podfile.lock` 里写的是 `RNScreens (from '../node_modules/react-native-screens')` ——
它是 **development pod**，源码就地引用 `node_modules`，CocoaPods 只生成
`Target Support Files/RNScreens` 与 `Headers/{Public,Private}/RNScreens`，
**无论 pod install 跑没跑过，都不会在 `ios/Pods/` 下建同名目录。**

还有一层干扰：RN 0.87 默认启用预编译核心（`React-Core-prebuilt`），`ios/Pods` 顶层本来就只有
十来个条目，根本不是「一个 pod 一个目录」的形态。

> 差点因此把一个无效判据当成证据写进结论。**判据要取锁文件内容，不是 Pods 目录结构。**

### 收尾：搞清报错信息为什么不指向根因

build 和 Metro 都正常（离线 bundle 10.05s 成功；Metro 返回 200 / 4.87 MB，内容里确实有
`RN$AppRegistry`），所以问题一定在运行时的 JS 求值期。查 RN 源码后找到了完整的因果链（见下）。

## 根因

两个事实叠加。

**（1）原生模块缺席。** `pod install` 未执行 → 原生 pod 不在 Pods 工程 → 依赖的原生组件不存在。

**（2）`RN$AppRegistry` 是惰性安装的，导致报错信息远离根因。**

`react-native/index.js` 用惰性 getter 导出模块，`global.RN$AppRegistry` 不是
`require('react-native')` 时装的，而是 `Libraries/ReactNative/AppRegistry.js:25` 那句
`global.RN$AppRegistry = AppRegistry;` —— 它要等 `AppRegistry.registerComponent(...)` 被
**实际调用**时才求值。

Babel 编译后的 CJS 求值顺序：

```js
require('react-native');              // 惰性 getter，此时不装 global
require('@/app/App');                 // ← App.tsx 整条 import 链在这里求值
AppRegistry.registerComponent(...);   // ← 到这一行 RN$AppRegistry 才挂上
```

而 `react-native-screens` 的原生组件是在**模块作用域**就注册的：

```js
// node_modules/react-native-screens/lib/commonjs/fabric/ScreenContainerNativeComponent.js:9
var _default = exports.default =
  (0, _reactNative.codegenNativeComponent)('RNSScreenContainer', {});
```

于是只要 App.tsx 的 import 链在求值期抛错，`registerComponent` 就永远执行不到 →
`global.RN$AppRegistry` 从未安装 → 原生侧 `startSurface` 抛：

```cpp
// ReactCommon/react/renderer/uimanager/AppRegistryBinding.cpp:31
auto registry = global.getProperty(runtime, "RN$AppRegistry");
if (!registry.isObject())
  throw std::runtime_error("AppRegistryBinding::startSurface failed. Global was not installed.");
```

> **这句话的真实含义是「JS 入口在求值期就挂了」，不是「AppRegistry 配置错了」。**
> 看到它不要去查 AppRegistry —— 它把根因藏在了离根因最远的地方。

## 解决方案

```bash
bundle exec pod install
yarn ios
```

`pod install`：`Installing RNScreens (4.28.0)`，87 个 pod；`Podfile.lock` 里 RNScreens 计数 0 → 6。

## 经验总结

- **`yarn ios` / `react-native run-ios` 报 success ≠ App 能跑。** 只表示构建与 `simctl launch`
  调用没报错。验收必须**看进程是否存活 + 截图**。本例的截图是决定性证据：原生 Stack header「Home」
  由 `react-native-screens` 的 `RNSScreenStackHeaderConfig`（Fabric 原生组件）渲染，
  它能画出来就证明原生侧接上了。
- **「加了原生依赖要重建」是个不完整的直觉 —— 少了一半。** 完整动作是
  **先 `pod install` 再重建**。只重建的话，缺的原生代码永远补不上，而且会让人误判为
  「重建没用，问题在别处」，把排查带偏。
- **`AppRegistryBinding::startSurface failed. Global was not installed.` 的真义是
  「JS 入口求值期抛错」**。顺着 RN 的惰性 getter 机制可以推出：任何在 `require('@/app/App')`
  期间抛出的异常，都会伪装成这个 AppRegistry 错误。
- **区分「development pod」和「普通 pod」的目录形态。** 前者源码在 `node_modules`，
  CocoaPods 不为它在 `ios/Pods/` 下建目录。用它当「pod 装没装」的判据会得到假阴性。
  **正确判据是 `grep <PodName> ios/Podfile.lock`。**
- **`pod install` 后必须 `git diff` 复查 `AppDelegate.swift` 与 `Info.plist`。**
  本例这两个文件带有手工的 UIScene 生命周期修复（RN 0.87 模板在 iOS 26+ 会启动即崩），
  一旦被 pod install 覆盖就会生成一个症状完全不同、但同样「启动即崩」的新 bug。
  本次复查：`pod install` 只改了 `Podfile.lock`，手工修复完好。
- **这类坑的触发面很宽**：`react-native-screens`、`react-native-svg`、
  `@react-native-async-storage/async-storage`、`react-native-safe-area-context` 都带原生代码，
  常被一次性批量 `yarn add`，只记得改 `package.json` 而漏掉 `pod install`。

## 相关 Skills

- troubleshooting
- bug-fix
- superpowers:systematic-debugging
