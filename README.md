# AI Engineering Specs

## 1. 项目定位

本仓库是个人/团队统一的 AI 软件工程规范与能力库（AI Engineering System）。

目标是让 AI Coding Agent 在不同项目、不同技术栈、不同开发任务中，遵循统一且可复用的工程流程，而不是每个项目重新编写一套 AI 指令。

本仓库主要服务于：

* Vue / Vue 2 / Vue 3
* React
* TypeScript / JavaScript
* Node.js
* Java / Spring Boot
* Monorepo
* 微前端
* 前后端分离项目
* 其他后续接入的技术栈

核心原则：

> Global Rules + Project Context + Task Skill + Stack Skill + Verification

即：

```text
全局工程规则
    +
项目 AGENTS.md
    +
任务 Skill
    +
技术栈 Skill
    +
自动验证
```

AI 不应该仅仅“生成代码”，而应该按照完整的软件工程流程完成任务：

```text
Understand
    ↓
Explore
    ↓
Plan
    ↓
Implement
    ↓
Verify
    ↓
Review
    ↓
Summarize
```

---

## 2. 仓库目录职责

仓库采用固定的顶层结构，六个核心目录职责必须保持稳定：

| 目录           | 职责       | 核心问题     |
| ------------ | -------- | -------- |
| `rules/`     | 工程约束     | 应该怎么做    |
| `skills/`    | 工作能力     | 怎么完成某类工作 |
| `agents/`    | Agent 角色 | 谁来做      |
| `knowledge/` | 经验知识     | 以前遇到过什么  |
| `templates/` | 工作模板     | 按什么格式做   |
| `scripts/`   | 自动化工具    | 如何自动验证   |

不要因为增加某个技术栈而随意增加新的顶层分类。

> 上表之外的 `projects/`（项目配置/示例）为可选项，不属于六个核心目录。

---

## 3. Rules 规则体系

### 3.1 Rules 的职责

`rules/` 保存必须遵守的工程约束。

Rules 回答：

> “AI 在任何项目中都应该遵守什么原则？”

Rules 应该：

* 简洁
* 稳定
* 可长期复用
* 尽量与具体项目无关
* 尽量与具体业务无关
* 避免描述具体实现方案

### 3.2 Rule 优先级

规则发生冲突时，按照以下优先级处理：

```text
安全 / 合规要求
    ↓
项目 AGENTS.md
    ↓
全局 Rules
    ↓
Stack Skills
    ↓
Task Skills
    ↓
Agent 默认行为
```

如果项目自己的 `AGENTS.md` 明确规定了某项特殊行为，应优先遵循项目规则。

但项目规则不能违反安全、合规以及更高层级的系统约束。

---

## 4. Skills 能力体系

### 4.1 Skills 的职责

`skills/` 保存 AI 完成特定任务所需要的工作方法。

Skills 回答：

> “这类工作应该怎么完成？”

目录固定分为：

```text
skills/
├── task/
└── stack/
```

### 4.2 Task Skills

`skills/task/` 描述任务类型。典型任务包括新功能开发、Bug 修复、重构、Code Review、故障排查。

Task Skill 不应该绑定某个具体技术栈。例如 `bug-fix` 描述的是：

```text
如何定位 Bug
如何复现
如何分析根因
如何制定修复方案
如何验证
如何避免回归
```

而不是：

```text
Vue Bug 应该怎么修
```

---

## 5. Stack Skills

`skills/stack/` 描述技术栈能力。

Stack Skill 回答：

> “在这个技术环境中，应该注意什么？”

Task Skill 和 Stack Skill 可以组合使用。例如：

```text
Bug 修复 React 项目

=
bug-fix
+
troubleshooting
+
react
+
项目 AGENTS.md
+
global rules
```

---

## 6. Agents 角色体系

`agents/` 用于定义不同 AI Agent 的职责。

### Planner

负责：

* 理解需求
* 分析代码
* 制定实施计划
* 识别风险
* 明确验收标准

不应该直接进行大规模代码修改。

### Developer

负责：

* 根据计划修改代码
* 遵循项目规范
* 编写测试
* 执行验证

### Reviewer

负责：

* 检查实现
* 检查潜在 Bug
* 检查边界条件
* 检查测试覆盖
* 检查安全问题
* 检查是否引入不必要的复杂度

### Debugger

负责：

* 分析异常
* 构建最小复现
* 定位根因
* 提出修复方案
* 验证修复结果

---

## 7. Knowledge 知识体系

`knowledge/` 保存已经解决过的问题、技术经验和故障记录。

Knowledge 与 Rules 的区别：

```text
Rules
    ↓
以后必须遵守的规则

Knowledge
    ↓
以前发生过的问题及解决经验
```

例如：

```text
knowledge/build/react-pdf-private-class.md
```

> ⚠️ 原 `AGENTS.md` 在此处截断——「可以记录：」的示例写到 `问题：` / `react-` 就中断了，未写完。
>
> <!-- TODO: 补全 Knowledge 条目的字段定义。可参考 skills/task/troubleshooting/SKILL.md 的「记录解决方案」一节。 -->

---

## 8. 实现状态

### 8.1 状态说明

| 标记 | 含义 |
| --- | --- |
| ✅ 已实现 | 文件已创建，正文与 frontmatter 均完整 |
| TODO | 尚未创建 |

**进度：16 / 33 个文件已创建**，另有 10 个空目录未建。

### 8.2 目录结构（实现中）

```
ai-engineering-specs/
│
├── README.md                                             # ✅ 已实现
│
├── rules/                                                # “应该怎么做”——约束 AI 行为
│   ├── global/                                           # 所有项目通用
│   │   ├── coding.md                                     # ✅ 已实现
│   │   ├── git.md                                        # ✅ 已实现
│   │   ├── testing.md                                    # ✅ 已实现
│   │   ├── security.md                                   # ✅ 已实现
│   │   └── ai-workflow.md                                # ✅ 已实现
│   │
│   ├── frontend/                                         # 前端通用规则          （整个目录未创建）
│   │   ├── coding.md                                     # TODO
│   │   ├── compatibility.md                              # TODO
│   │   └── ui.md                                         # TODO
│   │
│   ├── backend/                                          # 后端通用规则          （整个目录未创建）
│   │   ├── coding.md                                     # TODO
│   │   ├── api.md                                        # TODO
│   │   └── database.md                                   # TODO
│   │
│   └── monorepo/                                         # Monorepo 通用规则     （整个目录未创建）
│       └── structure.md                                  # TODO
│
├── skills/                                               # “怎么完成某类工作”——能力
│   │
│   ├── task/                                             # 按任务类型
│   │   ├── feature-development/
│   │   │   └── SKILL.md                                  # ✅ 已实现
│   │   ├── bug-fix/
│   │   │   └── SKILL.md                                  # ✅ 已实现
│   │   ├── refactor/
│   │   │   └── SKILL.md                                  # ✅ 已实现
│   │   ├── code-review/
│   │   │   └── SKILL.md                                  # ✅ 已实现
│   │   └── troubleshooting/
│   │       └── SKILL.md                                  # ✅ 已实现
│   │
│   └── stack/                                            # 按技术栈
│       ├── vue/
│       │   └── SKILL.md                                  # ✅ 已实现
│       ├── react/
│       │   └── SKILL.md                                  # ✅ 已实现
│       ├── node/
│       │   └── SKILL.md                                  # ✅ 已实现
│       ├── java/
│       │   └── SKILL.md                                  # ✅ 已实现
│       └── monorepo/
│           └── SKILL.md                                  # ✅ 已实现
│
├── agents/                                               # “谁来做”——Agent 角色    （整个目录未创建）
│   ├── planner/
│   │   └── AGENT.md                                      # TODO
│   ├── developer/
│   │   └── AGENT.md                                      # TODO
│   ├── reviewer/
│   │   └── AGENT.md                                      # TODO
│   └── debugger/
│       └── AGENT.md                                      # TODO
│
├── knowledge/                                            # “以前遇到过什么”——经验知识  （整个目录未创建）
│   ├── frontend/                                         # TODO
│   ├── backend/                                          # TODO
│   ├── build/                                            # TODO
│   ├── dependency/                                       # TODO
│   └── troubleshooting/                                  # TODO
│
├── templates/                                            # AI 工作模板           （整个目录未创建）
│   ├── AGENTS.md                                         # TODO
│   ├── task.md                                           # TODO
│   ├── bug.md                                            # TODO
│   └── review.md                                         # TODO
│
├── scripts/                                              # 自动化脚本            （整个目录未创建）
│   ├── verify.sh                                         # TODO
│   └── detect-project.sh                                 # TODO
│
└── projects/                                             # 可选：项目配置/示例    （整个目录未创建）
    ├── vue/                                              # TODO
    ├── react/                                            # TODO
    ├── node/                                             # TODO
    ├── java/                                             # TODO
    └── monorepo/                                         # TODO
```
