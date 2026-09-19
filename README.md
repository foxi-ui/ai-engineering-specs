# AI Engineering System

个人 / 团队 AI 软件工程能力库。

用于统一管理和沉淀 AI Coding Agent 在软件开发过程中的：

* 工程规则（Rules）
* 工作能力（Skills）
* Agent 角色（Agents）
* 技术经验（Knowledge）
* 工作模板（Templates）
* 自动化工具（Scripts）

目标不是建立一个庞大的 Prompt 仓库，而是逐步形成一套：

> **可复用、可验证、可持续演进的 AI 软件工程系统。**

---

# 1. Quick Start

如果第一次使用本项目，不需要先理解全部目录。

按照下面流程即可开始。

---

## 1.1 获取仓库

例如放在统一的 AI 工程目录：

```bash
mkdir -p ~/workspace/ai
cd ~/workspace/ai

git clone <your-ai-engineering-repository> my-ai-engineering
cd my-ai-engineering
```

如果仓库已经存在：

```bash
cd ~/workspace/ai/my-ai-engineering
git pull
```

---

## 1.2 检查目录

```bash
find . -maxdepth 2 -type d | sort
```

预期：

```text
.
./agents
./knowledge
./rules
./scripts
./skills
./templates
```

检查核心规则：

```bash
find rules -type f | sort
```

检查 Skills：

```bash
find skills -name "SKILL.md" | sort
```

---

## 1.3 第一个项目接入

进入一个实际项目：

```bash
cd ~/workspace/project-vue
```

首先确认项目当前状态：

```bash
git status
```

然后创建：

```bash
touch AGENTS.md
```

编辑：

```bash
vim AGENTS.md
```

或者使用 VS Code：

```bash
code AGENTS.md
```

项目 `AGENTS.md` 至少填写：

````markdown
# AGENTS.md

## 项目

项目名称：

项目用途：

## 技术栈

- Framework:
- Language:
- Node:
- Package Manager:

## 常用命令

开发：

```bash
npm run dev
````

测试：

```bash
npm test
```

构建：

```bash
npm run build
```

Lint：

```bash
npm run lint
```

## 项目结构

```text
src/
├── ...
```

## 开发约束

* ...
* ...

## 注意事项

* ...

````

可以直接复制：

```bash
cp ~/workspace/ai/my-ai-engineering/templates/AGENTS.md ./AGENTS.md
````

然后根据实际项目修改。

---

# 2. 第一次让 AI 使用

项目接入之后，进入项目目录：

```bash
cd ~/workspace/project-vue
```

然后启动 AI Coding Agent。

例如：

```bash
claude
```

或者使用你正在使用的其他 AI Coding Agent。

第一条任务不要直接让 AI 改代码。

建议先：

```text
阅读项目 AGENTS.md，并分析当前项目结构。

不要修改代码。

告诉我：
1. 项目技术栈
2. 项目启动方式
3. 构建方式
4. 测试方式
5. 主要目录结构
6. 当前项目有哪些特殊开发约束
```

确认 AI 正确理解项目后，再开始实际任务。

---

# 3. 第一个实际任务

例如：

```text
帮我修复当前项目的一个构建问题。

先不要修改代码。

请按照以下流程：
1. 阅读 AGENTS.md
2. 分析项目结构
3. 找到构建入口
4. 定位错误相关代码
5. 分析根因
6. 给出修复方案
7. 等我确认后再修改
```

确认方案后：

```text
按照刚才的方案实施。

要求：
1. 只修改必要文件
2. 不进行无关重构
3. 修改完成后执行项目已有的验证命令
4. 最后汇总修改文件和验证结果
```

---

# 4. 如何使用 Skills

Skills 不应该全部复制到项目中。

AI 根据任务选择需要的 Skill。

例如：

## Vue 新功能

使用：

```text
rules/global/*
+
skills/task/feature-development/
+
skills/stack/vue/
+
项目 AGENTS.md
```

## React Bug

使用：

```text
rules/global/*
+
skills/task/bug-fix/
+
skills/task/troubleshooting/
+
skills/stack/react/
+
项目 AGENTS.md
```

## Java API

使用：

```text
rules/global/*
+
skills/task/feature-development/
+
skills/stack/java/
+
项目 AGENTS.md
```

---

# 5. 手动指定 Skill

如果当前 AI Agent 没有自动加载机制，可以直接告诉 AI：

```text
请按照以下 Skill 执行：

~/workspace/ai/my-ai-engineering/skills/task/bug-fix/SKILL.md

同时参考：

~/workspace/ai/my-ai-engineering/skills/task/troubleshooting/SKILL.md

~/workspace/ai/my-ai-engineering/skills/stack/vue/SKILL.md
```

也可以先让 AI 阅读：

```text
请读取：

~/workspace/ai/my-ai-engineering/rules/global/ai-workflow.md

~/workspace/ai/my-ai-engineering/skills/task/bug-fix/SKILL.md

~/workspace/ai/my-ai-engineering/skills/stack/vue/SKILL.md

然后按照这些规范执行当前任务。
```

---

# 6. 推荐的日常开发命令

进入业务项目：

```bash
cd ~/workspace/project
```

开始任务之前：

```bash
git status
git diff
```

启动 AI：

```bash
claude
```

或者使用其他 AI Coding Agent。

---

## 6.1 新功能

告诉 AI：

```text
执行一个新功能开发任务。

请使用：
- feature-development Skill
- 当前项目对应 Stack Skill
- 当前项目 AGENTS.md

按照：
Understand → Explore → Plan → Implement → Verify → Review

执行。

在修改代码之前先给出计划。
```

---

## 6.2 Bug 修复

```text
执行 Bug 修复。

请使用：
- bug-fix Skill
- troubleshooting Skill
- 当前项目 Stack Skill
- 当前项目 AGENTS.md

先复现和定位根因，不要直接修改代码。

确认根因后给出修复方案。
```

---

## 6.3 重构

```text
执行代码重构。

请使用：
- refactor Skill
- 当前项目 Stack Skill
- 当前项目 AGENTS.md

要求：
1. 保持现有功能不变
2. 明确重构范围
3. 不进行无关修改
4. 重构后执行验证
```

---

## 6.4 Code Review

```text
对当前修改执行 Code Review。

请使用：
- code-review Skill
- 当前项目 Stack Skill
- 当前项目 AGENTS.md

重点检查：
1. 正确性
2. 边界条件
3. 测试
4. 性能
5. 安全
6. 可维护性
7. 是否存在无关修改
```

---

# 7. 推荐的验证命令

不同项目的验证命令不同。

优先使用项目 `AGENTS.md` 中定义的命令。

例如 Vue / React / Node：

```bash
npm run lint
npm run test
npm run build
```

pnpm：

```bash
pnpm lint
pnpm test
pnpm build
```

yarn：

```bash
yarn lint
yarn test
yarn build
```

Java：

```bash
./mvnw test
./mvnw package
```

或者：

```bash
mvn test
mvn package
```

Gradle：

```bash
./gradlew test
./gradlew build
```

Monorepo：

```bash
pnpm lint
pnpm test
pnpm build
```

实际命令以项目 `AGENTS.md` 为准。

---

# 8. 使用 verify.sh

当项目具备统一验证方式后，可以使用：

```text
scripts/verify.sh
```

执行：

```bash
~/workspace/ai/my-ai-engineering/scripts/verify.sh
```

如果脚本设计为接受项目路径：

```bash
~/workspace/ai/my-ai-engineering/scripts/verify.sh ~/workspace/project
```

如果当前版本的 `verify.sh` 尚未支持自动识别项目，请先使用项目自己的：

```bash
npm run lint
npm test
npm run build
```

不要为了使用统一脚本而修改项目原有验证方式。

---

# 9. 新问题如何沉淀

假设今天遇到：

```text
React + CRACO + react-pdf
```

导致：

```text
Cannot parse private class method
```

解决并验证之后，不要马上修改 Global Rule。

首先记录：

```text
knowledge/build/react-pdf-private-class.md
```

创建：

```bash
mkdir -p knowledge/build

touch knowledge/build/react-pdf-private-class.md
```

编辑：

```bash
code knowledge/build/react-pdf-private-class.md
```

记录：

```text
问题
环境
现象
复现
排查过程
根因
解决方案
验证
风险
适用范围
```

---

# 10. Knowledge → Skill

如果类似问题不断出现：

```text
第一次：
Webpack 构建失败

第二次：
Babel Parser 问题

第三次：
Loader 兼容问题

第四次：
第三方依赖语法问题
```

发现它们可以使用统一流程排查：

```text
检查错误位置
    ↓
检查依赖版本
    ↓
检查 Node
    ↓
检查构建工具
    ↓
检查 Loader
    ↓
检查 Parser
    ↓
检查 Babel
    ↓
检查配置
    ↓
最小复现
    ↓
验证
```

那么应该升级为 Skill。

例如：

```text
skills/task/troubleshooting/SKILL.md
```

---

# 11. Skill → Rule

如果经过多个项目、多个任务验证后，形成稳定的通用原则：

```text
修改代码前必须检查 git status / git diff
```

可以进入：

```text
rules/global/git.md
```

判断标准：

> 是否已经成为所有相关项目都应该遵守的长期规则？

如果只是某个项目：

```text
project/AGENTS.md
```

如果只是某种任务：

```text
skills/task/
```

不要把局部经验提升成 Global Rule。

---

# 12. 如何新增 Knowledge

创建目录：

```bash
mkdir -p knowledge/<category>
```

例如：

```bash
mkdir -p knowledge/frontend
mkdir -p knowledge/backend
mkdir -p knowledge/build
mkdir -p knowledge/dependency
mkdir -p knowledge/troubleshooting
```

创建文件：

```bash
touch knowledge/build/webpack-parser-error.md
```

然后编辑：

```bash
code knowledge/build/webpack-parser-error.md
```

---

# 13. 如何新增 Skill

例如新增：

```text
dependency-upgrade
```

执行：

```bash
mkdir -p skills/task/dependency-upgrade
touch skills/task/dependency-upgrade/SKILL.md
```

推荐结构：

```markdown
# Dependency Upgrade

## Goal

## When to Use

## Preconditions

## Workflow

### 1. Inspect Current Versions

### 2. Check Compatibility

### 3. Plan Upgrade

### 4. Implement

### 5. Verify

### 6. Review

## Failure Handling

## Output
```

---

# 14. 如何新增 Stack Skill

例如增加 Docker：

```bash
mkdir -p skills/stack/docker
touch skills/stack/docker/SKILL.md
```

例如增加 Spring Boot：

```bash
mkdir -p skills/stack/spring-boot
touch skills/stack/spring-boot/SKILL.md
```

例如增加 qiankun：

```bash
mkdir -p skills/stack/qiankun
touch skills/stack/qiankun/SKILL.md
```

原则：

```text
Task Skill
=
做什么

Stack Skill
=
在什么技术环境下做
```

---

# 15. 如何新增 Rule

例如增加 API 规范：

```bash
mkdir -p rules/backend
touch rules/backend/api.md
```

增加前端兼容性规则：

```bash
mkdir -p rules/frontend
touch rules/frontend/compatibility.md
```

但是新增 Rule 前先问：

```text
这个规则是否应该被多个项目长期遵守？
```

如果不是：

```text
不要放 Global Rule。
```

---

# 16. 如何新增 Agent

例如新增：

```text
performance-review
```

创建：

```bash
mkdir -p agents/performance-review
touch agents/performance-review/AGENT.md
```

内容至少包括：

```markdown
# Performance Reviewer

## Role

## Responsibilities

## Input

## Workflow

## Checks

## Output

## Acceptance
```

Agent 负责定义：

> 角色。

Skill 负责定义：

> 工作方法。

两者不要混在一起。

---

# 17. 如何使用 Knowledge

当遇到问题时，不要只搜索互联网。

首先搜索自己的 Knowledge：

```bash
find knowledge -type f | sort
```

快速搜索关键词：

```bash
grep -Rni "react-pdf" knowledge/
```

例如：

```bash
grep -Rni "private class" knowledge/
```

如果找到：

```text
knowledge/build/react-pdf-private-class.md
```

先阅读：

```bash
cat knowledge/build/react-pdf-private-class.md
```

或者：

```bash
code knowledge/build/react-pdf-private-class.md
```

然后再结合当前项目版本判断是否适用。

---

# 18. 推荐使用 Git 管理

这个仓库本身应该使用 Git。

初始化：

```bash
cd ~/workspace/ai/my-ai-engineering

git init
```

第一次提交：

```bash
git add .
git commit -m "chore: initialize AI engineering system"
```

之后修改：

```bash
git status
git diff
```

确认：

```bash
git add .
git commit -m "docs: update AI engineering workflow"
```

---

# 19. 推荐远程同步

如果是个人使用：

```text
GitHub
GitLab
Gitea
```

均可。

例如：

```bash
git remote add origin <repository-url>
git branch -M main
git push -u origin main
```

以后：

```bash
git pull
```

和：

```bash
git push
```

即可同步。

---

# 20. 团队使用

团队共享时：

```text
开发者 A
    ↓
修改 Rules / Skills / Knowledge
    ↓
Git Push
    ↓
Team Repository
    ↓
其他开发者
    ↓
Git Pull
```

推荐：

```bash
git pull --rebase
```

修改后：

```bash
git add .
git commit -m "docs: add xxx knowledge"
git push
```

---

# 21. TeamAI 接入

基础目录稳定之后，可以接入 TeamAI。

推荐顺序：

```text
AI Engineering System
        ↓
Rules
Skills
Knowledge
AGENTS.md
        ↓
验证稳定
        ↓
TeamAI
        ↓
统一同步 / 分发
```

不要一开始就把所有问题交给 TeamAI。

先把：

```text
规则
能力
知识
目录
工作流程
```

设计稳定。

然后再使用 TeamAI 解决：

```text
跨 Agent 同步
团队共享
Skills 分发
Rules 管理
MCP
Agents
Hooks
```

---

# 22. MCP 接入

MCP 用于给 AI 提供外部能力。

例如：

```text
GitHub
数据库
浏览器
文件系统
Jira
飞书
内部 API
```

原则：

```text
Skill
    ↓
告诉 AI 怎么做

MCP
    ↓
给 AI 提供能力
```

不要用 MCP 替代 Skill。

例如：

```text
GitHub MCP
```

提供：

```text
查询 PR
查询 Issue
读取 Repository
```

而：

```text
code-review Skill
```

定义：

```text
如何进行 Code Review
```

---

# 23. Hooks / Automation

当发现 AI 每次都执行：

```text
检查 git status
读取项目类型
运行 lint
运行 test
运行 build
```

可以考虑 Hook / Script 自动执行。

例如：

```text
scripts/detect-project.sh
scripts/verify.sh
```

目标：

```text
人工步骤
    ↓
稳定步骤
    ↓
Script
    ↓
Hook
    ↓
自动执行
```

---

# 24. 新项目接入 Checklist

新项目第一次接入：

```text
[ ] 创建项目 AGENTS.md
[ ] 确认技术栈
[ ] 确认 Node / JDK 版本
[ ] 确认包管理器
[ ] 确认启动命令
[ ] 确认测试命令
[ ] 确认构建命令
[ ] 确认 Lint 命令
[ ] 描述目录结构
[ ] 描述架构
[ ] 描述特殊约束
[ ] 使用 AI 完成一次实际任务
[ ] 验证结果
[ ] 沉淀发现的问题
```

---

# 25. 每次开发任务 Checklist

开始：

```text
[ ] git status
[ ] 阅读项目 AGENTS.md
[ ] 判断 Task Skill
[ ] 判断 Stack Skill
[ ] 搜索相关 Knowledge
```

分析：

```text
[ ] Understand
[ ] Explore
[ ] Plan
```

开发：

```text
[ ] Implement
[ ] 小步修改
[ ] 不修改无关代码
```

验证：

```text
[ ] Type Check
[ ] Lint
[ ] Test
[ ] Build
[ ] Review
```

结束：

```text
[ ] git diff
[ ] 总结修改
[ ] 总结验证
[ ] 判断是否产生新 Knowledge
[ ] 判断是否需要更新 Skill / Rule
```

---

# 26. 每周维护

每周执行一次：

```bash
cd ~/workspace/ai/my-ai-engineering

git pull --rebase

find knowledge -type f | sort

find skills -name "SKILL.md" | sort

find rules -name "*.md" | sort
```

然后检查：

```text
[ ] 是否存在重复 Knowledge
[ ] 是否存在过时 Knowledge
[ ] 是否有 Skill 可以升级
[ ] 是否有 Rule 需要修改
[ ] 是否有步骤可以自动化
[ ] 是否存在无效文档
```

---

# 27. 推荐的完整工作方式

以后一个真实任务：

```text
用户需求
    ↓
进入项目
    ↓
git status
    ↓
读取项目 AGENTS.md
    ↓
选择 Task Skill
    ↓
选择 Stack Skill
    ↓
检索 Knowledge
    ↓
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
    ↓
Knowledge Review
    ↓
Git Commit
```

最终形成：

```text
项目开发
    ↓
AI 执行
    ↓
验证
    ↓
经验沉淀
    ↓
能力升级
    ↓
自动化
    ↓
下一次任务
```

---

# 28. 常用命令速查

## 查看系统

```bash
cd ~/workspace/ai/my-ai-engineering

find . -maxdepth 3 -type f | sort
```

## 查看 Rules

```bash
find rules -type f | sort
```

## 查看 Skills

```bash
find skills -name "SKILL.md" | sort
```

## 查看 Agents

```bash
find agents -name "AGENT.md" | sort
```

## 查看 Knowledge

```bash
find knowledge -type f | sort
```

## 搜索经验

```bash
grep -Rni "关键词" knowledge/
```

## 搜索 Rule

```bash
grep -Rni "关键词" rules/
```

## 搜索 Skill

```bash
grep -Rni "关键词" skills/
```

## 查看 Git 状态

```bash
git status
```

## 查看修改

```bash
git diff
```

## 更新 AI Engineering System

```bash
git pull --rebase
```

## 提交

```bash
git add .
git commit -m "docs: update AI engineering system"
git push
```

---

# 29. 最小使用方式

如果不想一次性搭建全部系统，实际上只需要：

```text
my-ai-engineering/
├── AGENTS.md
├── HOW-TO-DO.md
├── README.md
├── rules/
│   └── global/
├── skills/
│   ├── task/
│   └── stack/
└── knowledge/
```

然后：

```text
项目
  +
AGENTS.md
  +
Global Rules
  +
Task Skill
  +
Stack Skill
  +
Knowledge
```

就已经可以开始使用。

其他：

```text
agents/
templates/
scripts/
MCP
Hooks
TeamAI
```

随着实际需求逐步增加。

---

# 30. 一句话理解

这个项目的使用方式可以简化成：

```text
项目 AGENTS.md
        +
正确的 Rule
        +
正确的 Skill
        +
相关 Knowledge
        ↓
AI 开发
        ↓
自动验证
        ↓
Review
        ↓
沉淀经验
```

最终目标：

> **让每一次开发都不仅产生代码，还能够产生可复用的工程能力。**

---

# 31. 相关文档

| 文档             | 作用                         |
| -------------- | -------------------------- |
| `README.md`    | 快速了解和开始使用                  |
| `AGENTS.md`    | AI Engineering System 运行规则 |
| `HOW-TO-DO.md` | 系统建设、维护和经验沉淀               |
| `rules/`       | 全局工程规则                     |
| `skills/`      | 可复用工作能力                    |
| `agents/`      | Agent 角色                   |
| `knowledge/`   | 技术经验和问题记录                  |
| `templates/`   | 标准工作模板                     |
| `scripts/`     | 自动化脚本                      |

---

# 32. 最终目标

```text
第一次遇到问题
        ↓
人 + AI 解决
        ↓
验证
        ↓
Knowledge

第二次遇到
        ↓
AI 查询 Knowledge
        ↓
快速解决

重复出现
        ↓
形成 Skill

经过验证
        ↓
形成 Rule

重复执行
        ↓
Script / Hook

最终
        ↓
AI Engineering System
不断进化
```

> **不是让 AI 一开始就知道所有东西，而是让系统能够持续积累正确的东西。**
