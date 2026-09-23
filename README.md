# AI Engineering Specs

团队共享的 AI Coding 工程能力库。

用于沉淀和复用：

- 开发规范
- Task Skills
- Stack Skills
- Knowledge
- AI 工程实践

核心目标：

让 AI 在正确的上下文中，以稳定、可验证的方式完成软件开发任务。


## 1. Structure

ai-engineering-specs/
├── README.md
├── AGENTS.md
├── HOW-TO-DO.md
├── teamai.yaml
│
├── rules/
├── skills/
│   ├── task/
│   └── stack/
├── knowledge/
├── agents/
├── templates/
└── scripts/


### rules

必须遵守的开发约束。

rules/
├── global/
├── frontend/
├── backend/
└── monorepo/


### skills

可复用的 AI 工作能力。

skills/
├── task/
│   └── documentation-design/
│
└── stack/
    ├── vue/
    ├── react/
    ├── node/
    ├── java/
    └── monorepo/


### knowledge

经过实际问题验证的经验。


### agents

需要独立职责的 AI 角色。


### templates

可复用的输出模板。


### scripts

自动化检查和辅助工具。


## 2. Task + Stack

Skills 使用两个主要维度：

Task  = 做什么
Stack = 在什么技术环境下做

例如：

React 项目建立开发文档体系

task/documentation-design
+
stack/react


Vue 项目建立开发文档体系

task/documentation-design
+
stack/vue


不要为组合创建：

react-documentation-design
vue-documentation-design

避免 Skill 数量随着技术栈和任务类型产生组合爆炸。

Task Skill 描述工作方法，Stack Skill 描述技术环境，按需组合。


## 3. Project

业务项目自己的信息不应该全部进入本仓库。

每个项目维护自己的：

AGENTS.md

例如：

my-project/
├── AGENTS.md
├── .teamai/
├── .claude/
└── src/

项目 AGENTS.md 描述：

- 项目目的
- 技术栈
- 项目结构
- 开发命令
- 测试命令
- 构建命令
- 项目特殊约束

共享仓库负责通用能力，业务项目负责项目上下文。


## 4. TeamAI

本仓库适合作为 TeamAI Team Repo。

推荐通用能力使用 User Scope：

teamai init <repository-url> --scope user

检查：

teamai status
teamai list --source repo
teamai list --agent claude --verbose
teamai doctor

业务项目需要自己的 TeamAI 配置时，再使用 Project Scope。

原则：

通用能力
→ User Scope

项目专属能力
→ Project Scope


## 5. Typical Usage

一个实际 AI Coding 任务通常组合：

Project
+
Task Skill
+
Stack Skill
+
Relevant Knowledge
+
Required Rules

例如：

项目：React Admin

任务：建立开发文档体系

Project
+
task/documentation-design
+
stack/react
+
相关 Knowledge
+
项目 Rules

不要默认加载整个仓库。

只提供当前任务需要的上下文。


## 6. Knowledge

问题和经验按照以下方向沉淀：

开发
 ↓
问题
 ↓
解决
 ↓
Knowledge
 ↓
重复出现
 ↓
Skill / Rule

一次性问题：

Knowledge

稳定的工作方法：

Skill

团队必须遵守的约束：

Rule


## 7. Documentation

根目录三个文档职责不同：

README.md
→ 怎么使用这个系统

AGENTS.md
→ AI 如何修改这个仓库

HOW-TO-DO.md
→ 如何长期建设和维护这个系统

不要在三个文件中重复相同内容。


## 8. Contributing

新增内容前：

find skills -name "SKILL.md" | sort
find rules -type f | sort
find knowledge -type f | sort

先搜索已有能力，再决定是否新增。

修改后检查：

git status
git diff

确认：

- 没有重复内容
- 没有敏感信息
- 没有无关文件
- 内容已经经过实际验证


## 9. Principles

本项目遵循：

少而有用
按需加载
事实优先
避免重复
实际验证
持续沉淀

不要追求最大的 Skill 数量。

目标是：

用更少的上下文，让 AI 更稳定地完成软件开发任务。


## 10. Maintenance

长期维护方法：

HOW-TO-DO.md

项目 AI 修改规则：

AGENTS.md

具体开发能力：

skills/

开发规范：

rules/

经验沉淀：

knowledge/