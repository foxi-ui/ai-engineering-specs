---
name: feature-development
description: 开发新功能、新页面、新 API、新组件或新模块时的完整流程：理解需求、寻找现有实现、设计、实现、验证、Review
---

# Feature Development Skill

## 适用场景

用于：

- 新功能
- 新页面
- 新 API
- 新组件
- 新业务流程
- 新模块

---

## Workflow

### Step 1：理解需求

明确：

```text
输入
输出
业务规则
异常情况
权限要求
兼容要求
```

### Step 2：寻找现有实现

搜索：

- 类似功能
- 类似组件
- 类似 API
- 公共工具
- 类型定义
- 测试

优先复用。

### Step 3：设计

确定：

```text
数据流
组件边界
API 边界
状态管理
错误处理
```

复杂功能先输出简短设计方案。

### Step 4：实现

推荐顺序：

```text
核心逻辑
↓
错误处理
↓
边界情况
↓
UI / API 接入
↓
测试
```

### Step 5：验证

根据项目执行：

- TypeCheck
- Lint
- Test
- Build

### Step 6：Review

重点检查：

- 是否满足需求
- 是否遗漏边界
- 是否引入重复代码
- 是否破坏已有 API
- 是否存在权限问题
- 是否存在兼容问题

---

## 输出

```text
Feature:
Changed Files:
Implementation:
Tests:
Verification:
Risks:
```