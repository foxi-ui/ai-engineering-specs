# HOW-TO-DO

ai-engineering-specs 的持续建设、维护和知识沉淀指南。


## 1. Purpose

本文件用于说明：

- 如何新增 Skill
- 如何新增 Rule
- 如何沉淀 Knowledge
- 如何判断内容应该放在哪里
- 如何避免重复
- 如何让 AI 能力持续演进
- 如何控制 Context
- 如何淘汰无效内容

它不是日常开发规范。

它回答的是：

这个 AI Engineering System 应该如何长期建设？


## 2. Core Model

本项目使用：

Project
+
Task
+
Stack
+
Knowledge
+
Rules


Project
→ 当前业务项目

Task
→ 当前要完成什么工作

Stack
→ 当前主要技术环境

Knowledge
→ 过去验证过什么

Rule
→ 必须遵守什么


## 3. Where Should New Content Go?

新增内容时依次判断。


这是强制约束吗？

是
→ Rule


这是完成某类工作的标准方法吗？

是
→ Task Skill


这是某种技术环境下的开发方法吗？

是
→ Stack Skill


这是过去遇到的问题和经验吗？

是
→ Knowledge


这是固定输出格式吗？

是
→ Template


这是重复执行的自动化操作吗？

是
→ Script


这是需要独立职责的工作角色吗？

是
→ Agent


如果仍然无法判断：

暂时不要创建新的资源。

先记录到现有 Knowledge 或任务记录中。


## 4. Task Skill

位置：

skills/task/

用途：

描述如何完成一类开发工作。

例如：

feature-development
bug-fix
refactor
code-review
troubleshooting
documentation-design


### 4.1 When to Create

满足以下条件时考虑创建：

- 经常出现
- 流程相对稳定
- 可以跨项目复用
- AI 可以按照明确步骤执行
- 有明确的验证方法

不要因为一次特殊任务就创建 Skill。


### 4.2 Structure

推荐：

skills/task/<name>/
└── SKILL.md

基本结构：

# Skill Name

## Purpose

## When to Use

## Workflow

## Constraints

## Verification

## Common Problems


## 5. Stack Skill

位置：

skills/stack/

用途：

描述某种主要技术环境下，AI 应该如何工作。

例如：

vue
react
node
java
monorepo


### 5.1 Stack Skill 的边界

Stack 不负责承载所有技术名词。

例如：

antd
webpack
vite
typescript
redis
mysql

不一定都应该创建成 Stack。

当前设计中：

Stack 只描述主要技术环境。


## 6. Task + Stack

不要创建：

react-bug-fix
vue-bug-fix
java-bug-fix
react-refactor
vue-refactor

而使用：

task/bug-fix
+
stack/react

或者：

task/refactor
+
stack/java

这样可以避免组合爆炸。


## 7. Knowledge

位置：

knowledge/

用途：

记录已经发生、已经分析、已经验证的问题和经验。

推荐分类：

knowledge/
├── frontend/
├── backend/
├── build/
├── dependency/
└── troubleshooting/


## 8. Knowledge 什么时候值得记录？

建议记录：

- 非显而易见的问题
- 排查过程有价值的问题
- 容易重复发生的问题
- 依赖升级踩坑
- 构建兼容问题
- 环境问题
- 项目架构经验
- AI Coding 中发现的有效方法

不建议记录：

- 简单查文档即可得到的信息
- 一次性的临时操作
- 没有验证过的猜测
- 没有复用价值的信息


## 9. Knowledge 推荐格式

# Problem

## Context

## Symptoms

## Cause

## Diagnosis

## Solution

## Verification

## Prevention

## Related

最重要的是记录：

为什么
怎么确认
怎么解决
如何验证

而不仅仅记录执行了什么命令。


## 10. Knowledge → Skill

如果发现：

同类问题
+
重复出现
+
解决流程稳定

就考虑提炼成 Skill：

Knowledge
↓
重复
↓
模式稳定
↓
Skill

例如：

多个项目反复出现依赖升级问题

可以沉淀：

skills/task/dependency-upgrade/


## 11. Knowledge → Rule

如果经验最终变成：

所有人都必须遵守的规则

则可以提升为 Rule。

例如：

禁止直接升级生产依赖

经过团队验证后，可以进入：

rules/global/

判断标准：

Knowledge
→ 建议记住

Skill
→ 可以复用的方法

Rule
→ 必须遵守的约束


## 12. Rule Design

Rule 应该少。

Rule 的特点：

- 稳定
- 强约束
- 跨项目
- 经常适用
- 违反后会产生明显风险

不要把普通建议全部变成 Rule。


## 13. Documentation Design

开发文档使用：

skills/task/documentation-design/

负责：

- README
- Architecture
- Development Guide
- API
- Deployment
- Troubleshooting
- 文档一致性检查

文档核心原则：

少而有用
事实优先
代码为源
持续验证
按需加载


## 14. Project-specific Knowledge

业务项目专属知识不要直接进入共享仓库。

例如：

- 某项目的业务流程
- 某公司的内部 API
- 某项目特殊部署方式
- 某项目历史遗留约束

优先放：

业务项目/
├── AGENTS.md
├── .teamai/
└── .claude/

只有当内容能够跨项目复用时，再提炼进入共享仓库。


## 15. Search Before Create

新增任何内容之前必须先搜索。

例如：

find skills -name "SKILL.md" | sort
find rules -type f | sort
find knowledge -type f | sort

搜索关键词：

grep -Rni "bug-fix" .
grep -Rni "dependency" .
grep -Rni "react" .

目标：

优先修改已有内容，而不是创建新文件。


## 16. Avoid Duplication

如果两个 Skill 有大量重复内容：

不要继续复制。

考虑：

公共 Rule
+
公共 Skill
+
各自特有内容

或者直接合并。


## 17. Skill Quality

Skill 不是越长越好。

一个好的 Skill 应该让 AI 快速知道：

- 什么时候使用
- 需要做什么
- 按什么顺序做
- 什么时候需要人工介入
- 如何验证

如果一个 Skill 越写越长：

优先考虑把背景知识拆到 Knowledge。


## 18. Context Management

本项目非常重视 Context 成本。

不要追求：

让 AI 知道一切。

应该追求：

让 AI 在当前任务知道正确的东西。

推荐：

Project
+
Task
+
Stack
+
Relevant Knowledge
+
Required Rules

而不是：

全部 Rules
+
全部 Skills
+
全部 Knowledge


## 19. Context Growth Review

如果发现 AI：

- 回复变慢
- Token 明显增加
- 工具调用增加
- 经常重复读取文件
- 开始忽略重要规则
- 输出质量下降

检查：

find rules -type f -exec wc -l {} \;
find skills -name "SKILL.md" -exec wc -l {} \;
find knowledge -type f -exec wc -l {} \;

重点检查：

- 是否有重复 Skill
- 是否有过长 Rule
- 是否把 Knowledge 写进 Skill
- 是否把项目知识放进共享 Skill
- 是否默认加载过多内容


## 20. Lifecycle

所有共享能力都应该有生命周期：

Candidate
↓
Created
↓
Used
↓
Verified
↓
Shared
↓
Maintained
↓
Deprecated
↓
Removed

进入 Git 不代表永久有效。


## 21. Candidate

不确定是否值得共享时：

不要马上创建正式 Skill。

可以先记录：

Knowledge

经过实际使用后再决定是否升级。


## 22. Verification

新 Skill 至少经过实际任务验证。

建议：

第一次使用
→ 观察

第二次使用
→ 修正

多项目使用
→ 判断是否通用

稳定后
→ 正式沉淀

不要只因为“看起来合理”就认为 Skill 有效。


## 23. Skill Review

定期检查：

这个 Skill 最近是否使用？

是否仍然适用？

是否有重复？

是否过长？

是否已经被代码工具替代？

是否产生了额外 Context 成本？

是否仍然能够提升 AI 输出质量？

如果没有价值：

修改
合并
降级为 Knowledge
或者删除


## 24. Rule Review

Rule 比 Skill 更应该谨慎。

如果 Rule：

- 很少使用
- 只适用于一个项目
- 只是建议
- 已经过时
- 与其他 Rule 重复

应该考虑删除或降级。


## 25. Contribution Workflow

新增或修改共享能力：

1. 明确问题
2. 搜索已有资源
3. 判断资源类型
4. 最小修改
5. 本地验证
6. 实际任务验证
7. Review
8. Commit
9. Push


## 26. Git Workflow

提交前：

git status
git diff

确认：

- 没有敏感信息
- 没有 Token
- 没有本地绝对路径
- 没有无关文件
- 没有重复内容

推荐提交：

feat: add documentation-design skill
fix: correct react skill guidance
docs: update knowledge workflow
refactor: simplify global rules


## 27. TeamAI Workflow

推荐：

本地修改
↓
实际项目验证
↓
Git Commit
↓
Team Repo
↓
TeamAI Pull
↓
其他项目使用
↓
反馈
↓
继续优化

不要把未经验证的实验性内容直接作为团队默认能力。


## 28. Periodic Maintenance

每周检查：

- 新增 Knowledge
- 新增 Skill
- 明显重复内容
- 近期发现的问题


每月检查：

- Skill 使用情况
- Rule 是否仍然有效
- 过长内容
- 重复内容
- 过时内容
- Context 成本


重大技术升级时检查：

- Stack Skill
- Knowledge
- Rules
- Templates
- Scripts


## 29. Golden Rules

1. 先搜索，再创建
2. 优先复用，避免重复
3. 一次问题先进入 Knowledge
4. 重复问题再提炼 Skill
5. 强制约束才成为 Rule
6. 项目专属内容不要进入共享仓库
7. Skill 越短越容易维护
8. Knowledge 不要塞进运行时上下文
9. 所有共享能力都必须经过验证
10. 不要为了完整而增加复杂度


## 30. Final Loop

业务开发
↓
问题
↓
Knowledge
↓
重复问题
↓
稳定解决方法
↓
Skill / Rule
↓
Team Repository
↓
更多项目复用
↓
新的问题
↓
Knowledge

最终目标：

让 AI Engineering System 持续从真实开发中获得反馈，并将有效经验转化为可复用能力。

不是追求最多的 Skills。

而是：

更少的 Context
+
更高的复用率
+
更稳定的 AI 输出