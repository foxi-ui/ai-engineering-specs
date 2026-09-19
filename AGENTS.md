# AGENTS.md

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

# 2. 仓库目录职责

仓库采用以下固定顶层结构：

```text
my-ai-engineering/
├── AGENTS.md
├── README.md
│
├── rules/
├── skills/
├── agents/
├── knowledge/
├── templates/
└── scripts/
```

六个核心目录职责必须保持稳定。

| 目录           | 职责       | 核心问题     |
| ------------ | -------- | -------- |
| `rules/`     | 工程约束     | 应该怎么做    |
| `skills/`    | 工作能力     | 怎么完成某类工作 |
| `agents/`    | Agent 角色 | 谁来做      |
| `knowledge/` | 经验知识     | 以前遇到过什么  |
| `templates/` | 工作模板     | 按什么格式做   |
| `scripts/`   | 自动化工具    | 如何自动验证   |

不要因为增加某个技术栈而随意增加新的顶层分类。

---

# 3. Rules 规则体系

## 3.1 Rules 的职责

`rules/` 保存必须遵守的工程约束。

Rules 回答：

> “AI 在任何项目中都应该遵守什么原则？”

例如：

```text
rules/global/coding.md
rules/global/git.md
rules/global/testing.md
rules/global/security.md
rules/global/ai-workflow.md
```

Rules 应该：

* 简洁
* 稳定
* 可长期复用
* 尽量与具体项目无关
* 尽量与具体业务无关
* 避免描述具体实现方案

---

## 3.2 Rule 优先级

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

# 4. Skills 能力体系

## 4.1 Skills 的职责

`skills/` 保存 AI 完成特定任务所需要的工作方法。

Skills 回答：

> “这类工作应该怎么完成？”

目录固定分为：

```text
skills/
├── task/
└── stack/
```

---

## 4.2 Task Skills

`skills/task/` 描述任务类型。

例如：

```text
skills/task/
├── feature-development/
├── bug-fix/
├── refactor/
├── code-review/
└── troubleshooting/
```

典型任务包括：

* 新功能开发
* Bug 修复
* 重构
* Code Review
* 故障排查

Task Skill 不应该绑定某个具体技术栈。

例如：

```text
bug-fix
```

描述的是：

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

# 5. Stack Skills

`skills/stack/` 描述技术栈能力。

例如：

```text
skills/stack/
├── vue/
├── react/
├── node/
├── java/
└── monorepo/
```

Stack Skill 回答：

> “在这个技术环境中，应该注意什么？”

例如：

```text
Vue Skill
React Skill
Node Skill
Java Skill
Monorepo Skill
```

Task Skill 和 Stack Skill 可以组合使用。

例如：

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

# 6. Agents 角色体系

`agents/` 用于定义不同 AI Agent 的职责。

推荐角色：

```text
agents/
├── planner/
├── developer/
├── reviewer/
└── debugger/
```

角色职责：

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

# 7. Knowledge 知识体系

`knowledge/` 保存已经解决过的问题、技术经验和故障记录。

目录：

```text
knowledge/
├── frontend/
├── backend/
├── build/
├── dependency/
└── troubleshooting/
```

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

可以记录：

```text
问题：
react-pdf / pdfjs 使用 private class syntax，
旧版 CRA / Babel 无法解析。

环境：
React
CRA
CRACO
webpack
Babel

原因：
node_modules 中依赖使用了当前构建链不支持的语法。

解决方案：
......

验证：
......

注意：
升级 react-pdf 时需要重新确认 pdfjs 版本。
```

Knowledge 应尽量记录：

```text
问题
环境
现象
原因
排查过程
解决方案
验证结果
相关版本
注意事项
```

不要把一次性的临时操作直接提升为全局 Rule。

---

# 8. Templates 模板体系

`templates/` 用于统一 AI 工作产物格式。

例如：

```text
templates/
├── AGENTS.md
├── task.md
├── bug.md
└── review.md
```

典型模板包括：

### Task

```text
需求
背景
目标
影响范围
实施计划
验收标准
验证结果
```

### Bug

```text
问题描述
复现步骤
环境
现象
根因
修复方案
验证
回归风险
```

### Review

```text
变更范围
正确性
可维护性
性能
安全
测试
风险
建议
```

模板用于统一 AI 输出，不应该成为硬性工程规则。

---

# 9. Scripts 自动化体系

`scripts/` 保存可以自动执行的检查和辅助脚本。

例如：

```text
scripts/
├── verify.sh
└── detect-project.sh
```

其中：

```text
verify.sh
```

负责统一执行项目验证。

例如：

```text
类型检查
Lint
Unit Test
Build
必要的静态检查
```

`detect-project.sh` 用于识别项目技术栈，例如：

```text
Vue
React
Node
Java
Monorepo
```

AI 应优先使用项目已有的验证命令，而不是自行发明验证方式。

---

# 10. Project AGENTS.md

业务项目应该拥有自己的 `AGENTS.md`。

例如：

```text
workspace/
├── my-ai-engineering/
│
├── project-vue/
│   └── AGENTS.md
│
├── project-react/
│   └── AGENTS.md
│
├── project-node/
│   └── AGENTS.md
│
├── project-java/
│   └── AGENTS.md
│
└── project-monorepo/
    ├── AGENTS.md
    ├── packages/
    └── apps/
```

项目 `AGENTS.md` 只描述项目自身的信息：

```text
项目是什么
技术栈
目录结构
启动命令
构建命令
测试命令
代码规范
架构约束
特殊依赖
特殊限制
部署方式
常见问题
```

不要在项目 `AGENTS.md` 中复制整个全局规则体系。

---

# 11. Monorepo AGENTS.md

Monorepo 可以使用多层 `AGENTS.md`。

例如：

```text
monorepo/
├── AGENTS.md
│
├── apps/
│   ├── web/
│   │   └── AGENTS.md
│   │
│   └── admin/
│       └── AGENTS.md
│
└── packages/
    ├── ui/
    │   └── AGENTS.md
    │
    └── utils/
        └── AGENTS.md
```

原则：

```text
根 AGENTS.md
    ↓
整个 Monorepo 通用规则

子目录 AGENTS.md
    ↓
该项目 / Package 的特殊规则
```

越靠近实际修改文件的位置，规则越具体。

---

# 12. AI 工作流程

任何中等以上复杂度任务，默认执行：

```text
1. Understand
2. Explore
3. Plan
4. Implement
5. Verify
6. Review
7. Summarize
```

---

## 12.1 Understand

先明确：

```text
用户想解决什么问题？
最终结果是什么？
有哪些限制？
验收标准是什么？
```

如果需求存在明显歧义，不应该直接大规模修改代码。

---

## 12.2 Explore

修改代码之前，先了解：

```text
项目结构
相关模块
调用关系
配置文件
依赖版本
现有测试
已有实现
```

优先使用：

```text
搜索
阅读
调用关系分析
现有测试
Git history
```

避免没有依据地修改代码。

---

## 12.3 Plan

对于中大型任务，应先形成实施计划：

```text
目标
影响文件
实现步骤
风险
验证方式
```

计划应该尽量具体到：

```text
文件
模块
函数
配置
测试
```

---

## 12.4 Implement

实施阶段：

* 小步修改
* 优先复用已有实现
* 不无理由重构
* 不修改无关代码
* 保持 API 稳定
* 保持项目现有代码风格

如果发现需求与原计划存在明显偏差，应重新评估，而不是继续盲目执行原计划。

---

# 13. Verification 验证原则

AI 完成修改后必须验证。

最基本流程：

```text
修改
 ↓
类型检查
 ↓
Lint
 ↓
测试
 ↓
Build
 ↓
Review
```

具体执行哪些验证，由项目实际情况决定。

---

## 13.1 不允许只说“应该没问题”

AI 不应该使用以下形式代替验证：

```text
应该可以
看起来没问题
理论上没问题
应该不会影响其他地方
```

必须尽可能通过：

```text
测试
构建
静态检查
运行结果
日志
实际复现
```

获得证据。

---

## 13.2 验证失败

如果验证失败：

```text
失败
 ↓
分析原因
 ↓
修复
 ↓
重新验证
```

不要隐藏失败结果。

最终总结必须明确：

```text
已验证
未验证
验证失败
无法验证的原因
```

---

# 14. Bug 修复原则

Bug 修复优先采用：

```text
复现
 ↓
定位
 ↓
确认根因
 ↓
最小修改
 ↓
验证
 ↓
防回归
```

不要一看到异常就直接修改代码。

尤其注意：

```text
表象 ≠ 根因
```

例如：

```text
构建失败
```

不应该直接认为：

```text
某个依赖有问题
```

应该确认：

```text
错误位置
调用链
构建链
依赖版本
编译器能力
配置
实际触发条件
```

---

# 15. 重构原则

重构必须区分：

```text
功能修改
结构修改
技术升级
```

不要在一次 Bug 修复中顺便进行大规模重构。

如果确实需要重构，应明确：

```text
为什么重构
影响范围
收益
风险
验证方式
```

优先：

```text
小范围
可回滚
可验证
```

---

# 16. 依赖升级原则

依赖升级属于高风险任务。

升级之前必须确认：

```text
当前版本
目标版本
Node / Java 版本
构建工具版本
Peer Dependencies
Breaking Changes
```

升级之后至少执行：

```text
install
typecheck
lint
test
build
```

如果是核心依赖：

```text
React
Vue
webpack
Babel
TypeScript
Node
Spring Boot
JDK
```

应额外检查兼容性。

---

# 17. Git 原则

AI 不应该擅自：

```text
git reset --hard
git clean -fd
删除用户修改
覆盖未提交代码
```

除非用户明确要求并确认风险。

修改之前应关注：

```text
git status
git diff
```

避免覆盖用户已有工作。

提交代码时：

* Commit message 清晰
* 一个 Commit 尽量对应一个逻辑变更
* 不混入无关格式化
* 不提交临时文件
* 不提交密钥和敏感信息

---

# 18. 安全原则

禁止将以下内容提交到仓库：

```text
密码
API Key
Token
Private Key
数据库密码
生产环境凭证
Cookie
Session
个人敏感信息
```

发现疑似 Secret 时，应：

```text
停止传播
确认来源
建议轮换
清理 Git history（必要时）
```

不要把真实凭证写入：

```text
AGENTS.md
SKILL.md
Knowledge
README
代码
```

---

# 19. AI Context 管理

AI 的上下文应该遵循：

```text
必要信息优先
局部信息优先
当前任务优先
避免无关信息
```

不要为了让 AI “知道更多”而加载整个仓库。

推荐上下文：

```text
Global Rules
+
Project AGENTS.md
+
相关 Stack Skill
+
相关 Task Skill
+
相关 Knowledge
+
当前代码
```

而不是：

```text
整个知识库
+
所有 Skill
+
所有项目
```

---

# 20. Skill 加载原则

Skill 应按任务加载，而不是全部加载。

例如：

### Vue Bug

```text
global rules
+
bug-fix
+
troubleshooting
+
vue
+
project AGENTS.md
```

### React 新功能

```text
global rules
+
feature-development
+
react
+
project AGENTS.md
```

### Java API 修改

```text
global rules
+
feature-development
+
java
+
project AGENTS.md
```

### Monorepo 依赖升级

```text
global rules
+
dependency / relevant task skill
+
monorepo
+
project AGENTS.md
```

---

# 21. Knowledge 沉淀原则

一个问题满足以下条件时，可以沉淀到 `knowledge/`：

```text
1. 具有重复发生的可能
2. 排查过程具有参考价值
3. 解决方案不容易从官方文档直接得到
4. 对未来项目有帮助
```

不要把所有普通 Bug 都记录下来。

Knowledge 的目标不是：

> 记录一切。

而是：

> 记录未来可以减少重复思考的经验。

---

# 22. 新增规则的判断标准

不要轻易新增 Rule。

新增 Rule 前先问：

```text
这个问题是否会在多个项目重复出现？
```

如果：

```text
是
```

考虑：

```text
Rule
```

如果：

```text
只是某个技术栈
```

考虑：

```text
Stack Skill
```

如果：

```text
只是某类任务
```

考虑：

```text
Task Skill
```

如果：

```text
只是某次问题经验
```

考虑：

```text
Knowledge
```

如果：

```text
只是输出格式
```

考虑：

```text
Template
```

如果：

```text
可以自动执行
```

考虑：

```text
Script / Hook
```

---

# 23. 避免规则膨胀

AI 工程体系必须避免：

```text
规则越来越多
→
上下文越来越大
→
AI 注意力下降
→
真正重要的规则反而被忽略
```

因此：

* Rule 尽量短
* Skill 按需加载
* Knowledge 按需检索
* Template 保持稳定
* 项目特殊规则放项目 `AGENTS.md`
* 不重复描述同一规则

---

# 24. 修改 AI Engineering System 的流程

修改本仓库自身时，也应该遵循：

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
```

新增规则、Skill、Agent 时，应明确：

```text
为什么新增？
解决什么问题？
适用范围？
是否与已有能力重复？
是否会增加 AI 上下文负担？
```

---

# 25. 新增文件命名规范

推荐：

```text
Rules:
*.md

Skills:
SKILL.md

Agents:
AGENT.md

Templates:
*.md

Knowledge:
*.md

Scripts:
可执行脚本文件
```

目录名称使用：

```text
kebab-case
```

例如：

```text
feature-development
code-review
dependency-upgrade
troubleshooting
```

---

# 26. 项目接入标准

一个新项目接入本 AI 工程体系时，最少需要：

```text
project/
└── AGENTS.md
```

并明确：

```text
项目名称
项目用途
技术栈
Node / JDK 等版本
包管理器
启动命令
开发命令
测试命令
构建命令
Lint 命令
目录结构
架构说明
特殊约束
```

推荐模板：

```text
templates/AGENTS.md
```

---

# 27. 推荐任务组合

## 新功能

```text
global rules
+
feature-development
+
对应 stack skill
+
project AGENTS.md
```

## Bug

```text
global rules
+
bug-fix
+
troubleshooting
+
对应 stack skill
+
project AGENTS.md
```

## 重构

```text
global rules
+
refactor
+
对应 stack skill
+
project AGENTS.md
```

## Code Review

```text
global rules
+
code-review
+
对应 stack skill
+
project AGENTS.md
```

## 复杂故障

```text
global rules
+
bug-fix
+
troubleshooting
+
stack skill
+
knowledge
+
project AGENTS.md
+
reviewer
```

---

# 28. Definition of Done

AI 任务完成的基本标准：

```text
[ ] 需求已经理解
[ ] 已检查相关代码
[ ] 已确认影响范围
[ ] 已制定合理方案
[ ] 修改范围符合需求
[ ] 没有无关修改
[ ] 类型检查通过（适用时）
[ ] Lint 通过（适用时）
[ ] 测试通过（适用时）
[ ] Build 通过（适用时）
[ ] 已进行必要的 Code Review
[ ] 没有明显安全问题
[ ] 没有遗留临时文件
[ ] 已说明验证结果
```

如果某项无法执行，应明确说明原因。

---

# 29. 最终原则

这个仓库不是“AI Prompt 集合”。

它应该逐渐成为：

```text
个人 / 团队的软件工程知识系统
            +
AI Agent 工作规范
            +
可复用开发能力
            +
自动化验证体系
```

最终形成：

```text
              my-ai-engineering
                       │
        ┌──────────────┼──────────────┐
        │              │              │
      Rules          Skills         Agents
        │              │              │
     约束体系       能力体系        角色体系
        │              │              │
        └──────────────┼──────────────┘
                       │
                   Knowledge
                       │
                    经验沉淀
                       │
              Templates / Scripts
                       │
                   标准化 + 自动化
                       │
                       ▼
              各个实际业务项目
                       │
          ┌────────────┼────────────┐
          ▼            ▼            ▼
        Vue          React         Java
          │            │            │
        Node         Monorepo      ...
```

核心目标：

> **让 AI 在不同项目中保持一致的工程质量，同时让具体项目保留自己的技术和业务特性。**

不要追求“让 AI 知道所有东西”，而应该追求：

> **让 AI 在正确的时间获得正确的上下文，并通过验证证明结果正确。**
