---
name: troubleshooting
description: 系统化定位复杂问题的流程：Collect、Reproduce、Classify、Narrow Down、Hypothesis、Verify、Fix、Regression，每次只验证一个假设，禁止未判断原因就删 node_modules 或升级依赖
---

# Troubleshooting Skill

## 目标

系统化定位复杂问题。

---

## 标准流程

```text
Collect
↓
Reproduce
↓
Classify
↓
Narrow Down
↓
Hypothesis
↓
Verify
↓
Fix
↓
Regression
```

---

## Collect

收集：

```text
Error
Stack Trace
Environment
Version
Command
Input
Expected
Actual
```

---

## Classify

首先判断问题类型：

```text
Code
Dependency
Build
Runtime
Environment
Network
Configuration
Data
Permission
```

---

## Narrow Down

逐步缩小范围：

```text
整个系统
↓
模块
↓
文件
↓
函数
↓
变量
```

---

## Hypothesis

每次只验证一个主要假设。

例如：

```text
假设：Node 版本导致依赖无法运行
```

验证：

```bash
node -v
```

然后根据结果确认或排除。

---

## 不要盲目尝试

禁止把下面操作作为第一反应：

```text
删 node_modules
删 lock
重新安装
升级所有依赖
```

必须先判断原因。

---

## 记录解决方案

解决复杂问题后建议记录：

```text
Problem
Environment
Symptom
Root Cause
Investigation
Solution
Failed Solutions
Scope
Keywords
```

用于后续 Knowledge Base。

---

## 输出

```text
Problem:
Root Cause:
Evidence:
Solution:
Verification:
Knowledge Worth Saving:
```
