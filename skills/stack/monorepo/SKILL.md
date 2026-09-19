---
name: monorepo
description: 在多 Package / 多 Application 仓库中安全修改代码：先定位 workspace 结构与依赖图，明确目标 Package 及其受影响的 Packages 与 Applications，按依赖顺序验证而非整体构建，不无意义修改 lockfile
---

# Monorepo Development Skill

## 目标

在多 Package / 多 Application 仓库中安全修改代码。

---

## 第一原则

先确定：

```text
Repository Root
↓
Workspace
↓
Application
↓
Package
↓
Dependency Graph
```

---

## 开始前检查

寻找：

```text
pnpm-workspace.yaml
package.json
turbo.json
nx.json
lerna.json
```

或者其他 workspace 配置。

---

## 确认修改范围

例如：

```text
apps/admin
apps/web
packages/ui
packages/utils
```

明确：

```text
Target Package
Affected Packages
Affected Applications
```

---

## Dependency Graph

修改公共 package 前检查：

```text
谁依赖它？
```

例如：

```text
packages/utils
    ↓
packages/ui
    ↓
apps/admin
    ↓
apps/web
```

公共 package 的修改可能影响大量项目。

---

## Lock File

不要无意义修改：

```text
pnpm-lock.yaml
package-lock.json
yarn.lock
```

只有依赖变化导致 lockfile 必须更新时才修改。

---

## Build

优先验证受影响 package：

```text
Changed Package
↓
Dependent Package
↓
Affected Application
```

不要一开始就构建整个 Monorepo。

---

## 版本

修改公共依赖时检查：

- workspace protocol
- peerDependencies
- dependencies
- devDependencies
- package version
- Node version

---

## 路径规则

如果仓库存在多个：

```text
AGENTS.md
CLAUDE.md
```

必须遵循离当前文件最近且适用的规则。

推荐优先级：

```text
Global Rules
↓
Repository Rules
↓
Application Rules
↓
Package Rules
↓
Task Skill
```

更具体的规则可以补充或覆盖通用规则。

---

## 验证

最终至少确认：

```text
Changed Package
Dependent Packages
Affected Applications
```

并执行对应：

```text
typecheck
lint
test
build
```

---

## 输出

```text
Changed:
Affected:
Verification:
Potential Impact:
```
