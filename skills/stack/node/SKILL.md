---
name: node
description: Node.js 服务端修改代码前的检查项：确认 Node 版本、包管理器与模块系统（ESM/CommonJS 不可混用），错误处理必须有明确策略而非 console.log，异步需考虑 rejection/timeout/retry/并发，禁止把 Secret 写入代码
---

# Node.js Development Skill

## 开始前检查

确认：

```text
Node version
Package Manager
Framework
TypeScript
Module System
```

例如：

```text
Node 18
Node 20
Node 22
```

不要假设环境版本。

---

## Package Manager

先确认：

```text
npm
pnpm
yarn
bun
```

不要在项目中混用。

---

## ESM / CommonJS

修改模块系统前确认：

- package.json
- type
- tsconfig
- build config
- runtime

不要随意混用：

```text
require
import
module.exports
export
```

---

## API

API 层应该明确：

```text
Request
↓
Validation
↓
Business Logic
↓
Response
↓
Error
```

---

## 错误处理

不要：

```ts
catch (error) {
  console.log(error)
}
```

必须确定明确的错误处理策略。

---

## 配置

环境变量区分：

```text
Development
Test
Production
```

禁止把 Secret 写入代码。

---

## 异步

优先：

```ts
async / await
```

注意：

- Promise rejection
- timeout
- retry
- cancellation
- concurrency

---

## 数据库

检查：

- SQL Injection
- Transaction
- Connection Pool
- N+1
- Pagination
- Index

---

## 验证

根据项目实际命令执行：

```text
typecheck
lint
test
build
```
