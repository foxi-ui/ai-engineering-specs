---
name: refactor
description: 在保持现有业务行为不变的前提下改善代码结构：明确 Refactor 边界、小步修改、保持 API 与行为、防止演变为 Rewrite
---

# Refactor Skill

## 目标

改善代码结构，同时保持现有业务行为不变。

---

## Refactor 前

必须确认：

- 当前行为
- 当前测试
- API
- 外部依赖
- 调用方

---

## 明确 Refactor 边界

定义：

```text
In Scope
Out of Scope
```

例如：

```text
In Scope:
拆分巨大 Service

Out of Scope:
修改数据库结构
修改 API
升级框架
```

---

## Refactor 原则

优先：

```text
小步修改
↓
运行测试
↓
继续修改
↓
再次测试
```

不要一次性大规模重写。

---

## 保持行为

重构前后应该保持：

- API
- 输入输出
- 错误行为
- 权限行为
- 数据结构
- 性能特征

除非用户明确要求改变。

---

## 检查

重点检查：

### API

是否改变？

### Behavior

业务行为是否改变？

### Dependency

依赖关系是否恶化？

### Complexity

复杂度是否真正下降？

### Test

测试是否覆盖核心行为？

---

## 禁止

不要把：

```text
Refactor
```

变成：

```text
Rewrite
```

除非用户明确要求重写。