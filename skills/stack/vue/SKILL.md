---
name: vue
description: Vue 2 / Vue 3 项目修改代码前的检查项：确认 Vue 版本与构建工具，严守 Vue 2 与 Vue 3 的 API 边界，Props/Emits 明确，异步请求覆盖 loading/error/empty，派生状态优先 computed，UI 改动沿用项目现有 Design System
---

# Vue Development Skill

## 适用

Vue 2 / Vue 3 项目。

---

## 开始前检查

确认：

- Vue version
- TypeScript
- Vite / Webpack / Vue CLI
- UI Library
- State Management
- Router
- Node version

---

## Vue 2

注意：

- Options API
- mixins
- filters
- Vue 2 reactivity
- lifecycle
- `$refs`

不要在 Vue 2 项目中直接使用 Vue 3 API。

---

## Vue 3

优先根据项目现有风格选择：

- Composition API
- Options API
- `<script setup>`

不要为了“现代化”无意义迁移。

---

## Components

组件应该：

- 单一职责
- Props 明确
- Emits 明确
- 避免过度耦合
- 避免组件承担过多业务逻辑

---

## TypeScript

优先：

```ts
interface
type
Props
Emits
```

避免：

```ts
any
```

---

## 异步请求

必须考虑：

- loading
- error
- empty
- retry
- race condition

---

## 响应式

合理使用：

- reactive
- ref
- computed
- watch
- watchEffect

避免不必要的 watch。

派生状态优先考虑：

```ts
computed
```

---

## UI 修改

修改 UI 前先确认项目现有：

- Design System
- UI Library
- spacing
- typography
- form pattern

不要重新创造一套风格。

---

## 验证

根据项目实际情况执行：

```bash
npm run typecheck
npm run lint
npm test
npm run build
```

实际命令以 `package.json` 为准。
