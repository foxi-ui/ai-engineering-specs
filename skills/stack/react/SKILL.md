---
name: react
description: React 项目修改代码前的检查项：确认 React 版本与构建工具，组件单一职责、Props 明确，避免滥用 useMemo/useCallback 与不必要的 useEffect+setState，状态按 Local → Feature → Global 分层，公共组件必须定义 Props 类型
---

# React Development Skill

## 开始前检查

确认：

- React version
- TypeScript
- CRA / Vite / Next.js / Webpack
- UI Library
- State Management
- Router
- Node version

---

## Components

组件应该：

- 单一职责
- 明确 Props
- 保持数据流清晰
- 避免巨型组件

---

## Hooks

合理使用：

```text
useState
useEffect
useMemo
useCallback
useRef
useContext
```

不要为了“优化”到处使用：

```text
useMemo
useCallback
```

必须有实际收益。

---

## useEffect

使用前确认是否真的需要 Effect。

不要把简单的派生状态写成：

```text
useEffect
↓
setState
```

优先考虑：

```text
直接计算
```

或者：

```text
useMemo
```

---

## State

状态优先级：

```text
Local State
↓
Feature State
↓
Global State
```

只有真正跨模块共享时才进入 Global State。

---

## 性能

检查：

- unnecessary render
- large list
- unstable props
- expensive calculation
- network waterfall
- bundle size

---

## TypeScript

避免无意义：

```ts
any
```

公共组件必须定义 Props。

---

## 兼容性

修改构建代码前检查：

- Babel
- Webpack
- Browserslist
- Node
- Polyfill

不要默认现代浏览器 API 一定可用。

---

## 验证

根据项目 `package.json` 执行：

```text
typecheck
lint
test
build
```
