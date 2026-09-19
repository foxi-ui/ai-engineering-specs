---
name: code-review
description: 审查代码改动的方法：按 Correctness、Edge Cases、Regression、Security、Performance、Maintainability 六项顺序检查，按 CRITICAL/HIGH/MEDIUM/LOW 分级输出，每个问题须含 Location、Problem、Why、Impact、Suggestion
---

# Code Review Skill

## Review 目标

Review 不是检查代码格式，而是发现：

- Bug
- 回归
- 安全问题
- 架构问题
- 性能问题
- 可维护性问题

---

## Review 顺序

### 1. Correctness

代码是否实现预期功能？

### 2. Edge Cases

检查：

- null
- undefined
- empty
- duplicate
- timeout
- exception
- concurrent requests

### 3. Regression

是否破坏已有功能？

### 4. Security

检查：

- 权限
- 输入校验
- XSS
- SQL Injection
- SSRF
- Secrets

### 5. Performance

检查：

- N+1
- 重复请求
- 大循环
- 不必要渲染
- 内存泄漏
- Bundle Size

### 6. Maintainability

检查：

- 命名
- 抽象
- 重复代码
- 复杂度
- 模块边界

---

## Review 输出

按严重程度：

```text
CRITICAL
HIGH
MEDIUM
LOW
```

但不要为了数量制造问题。

---

## 每个问题必须包含

```text
Location:
Problem:
Why:
Impact:
Suggestion:
```

---

## Review 结论

必须说明：

```text
Reviewed:
Risks:
Findings:
Verification:
```

不要只输出：

```text
LGTM
```
