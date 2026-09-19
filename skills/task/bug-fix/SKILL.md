---
name: bug-fix
description: 定位并修复缺陷的方法：收集信息、最小复现、调用链定位、确认根因、先写回归测试、最小修复、回归验证
---

# Bug Fix Skill

## 核心原则

不要直接猜原因。

遵循：

```text
现象
↓
复现
↓
定位
↓
根因
↓
最小修复
↓
回归验证
```

---

## Step 1：收集信息

确认：

- 错误信息
- Stack Trace
- 浏览器 / Node / Java 版本
- 依赖版本
- 触发条件
- 期望行为
- 实际行为

---

## Step 2：复现

优先建立最小复现。

记录：

```text
Input:
Environment:
Steps:
Expected:
Actual:
```

---

## Step 3：定位

检查：

- Stack Trace
- 调用链
- 数据流
- 条件判断
- 异步流程
- 第三方依赖
- 构建配置
- 环境差异

---

## Step 4：确认根因

不要把：

```text
错误位置
```

直接当成：

```text
根因
```

需要通过证据建立因果关系。

例如：

```text
TypeError
↓
调用 A
↓
A 参数来自 B
↓
B 在某条件下返回 undefined
```

真正根因可能是 B。

---

## Step 5：先写回归测试

如果条件允许：

```text
Bug Reproduction Test
```

应该先失败。

---

## Step 6：最小修复

只修改导致 Bug 的部分。

避免：

```text
修 Bug
↓
顺便重构
↓
顺便升级依赖
↓
顺便改架构
```

---

## Step 7：验证

至少：

```text
Bug Test
+
Related Tests
+
TypeCheck
+
Build（适用）
```

---

## 输出

```text
Bug:
Root Cause:
Fix:
Regression Test:
Verification:
Remaining Risk:
```