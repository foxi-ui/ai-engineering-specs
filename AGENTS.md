# AGENTS.md

## Project

ai-engineering-specs 是团队共享的 AI Coding 能力库。

主要维护：

rules/
skills/
knowledge/
agents/
templates/
scripts/


## Core Model

rules
→ 必须遵守的约束

skills
→ 可复用的工作能力

knowledge
→ 已验证的经验

agents
→ 独立职责

templates
→ 输出模板

scripts
→ 自动化工具


Skills 使用：

skills/task/
skills/stack/

task
→ 做什么

stack
→ 在什么主要技术环境下做

不要为 Task + Stack 的组合创建大量 Skill。


## Before Changes

修改前必须：

1. 阅读相关文件。
2. 搜索是否已有相同或相似内容。
3. 优先修改已有资源。
4. 确认新增内容具有复用价值。
5. 避免项目专属内容进入共享仓库。


## Resource Rules

Rule：

必须长期遵守的约束。

位置：

rules/


Task Skill：

描述如何完成某类工作。

位置：

skills/task/


Stack Skill：

描述某种主要技术环境。

位置：

skills/stack/


Knowledge：

记录已经验证的问题、原因和解决方案。

位置：

knowledge/


Agent：

只有存在独立职责时创建。


Template：

多个任务需要稳定输出格式时创建。


Script：

重复、确定性的操作优先自动化。


## Context

不要默认加载整个仓库。

优先使用：

Project
+
Task
+
Stack
+
Relevant Knowledge
+
Required Rules

避免：

全部 Rules
+
全部 Skills
+
全部 Knowledge


## Knowledge Promotion

一次问题：

Knowledge

重复且解决流程稳定：

Knowledge → Skill

形成团队强制约束：

Knowledge → Rule


## Project-specific Content

项目专属信息放在业务项目：

AGENTS.md
.teamai/
.claude/

不要未经验证直接加入共享能力。


## Verification

修改后检查：

git status
git diff

同时确认：

- Markdown 正确
- 路径正确
- 引用有效
- 无重复内容
- 无敏感信息
- 没有增加不必要的 Context


## Git

提交前确认：

- 没有 Token
- 没有密码
- 没有本地绝对路径
- 没有无关修改

使用清晰的 Commit：

feat: ...
fix: ...
docs: ...
refactor: ...


## Final Principle

先搜索
→ 优先复用
→ 最小修改
→ 实际验证
→ 再沉淀

目标不是增加资源数量。

目标是：

更少的 Context，更高的复用率，更稳定的 AI 输出。

详细维护方法：

HOW-TO-DO.md