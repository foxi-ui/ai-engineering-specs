# AI Engineering System 建设与沉淀指南

本文档用于指导 `ai-engineering-specs` 的持续建设。

主要解决两个问题：

1. 后续如何完善 AI Engineering System
2. 日常开发中的经验、规则、问题和解决方案如何沉淀

核心原则：

> 不追求一次性把体系建设完整，而是在真实开发过程中持续发现问题、解决问题、验证方案，再将高价值经验沉淀为可复用能力。

---

# 1. 整体建设原则

本仓库不是一次性完成的 Prompt 集合，而是一个持续演进的 AI 软件工程系统。

整体循环：

```text
实际开发
   ↓
发现问题
   ↓
解决问题
   ↓
验证结果
   ↓
判断是否值得沉淀
   ↓
选择正确的沉淀类型
   ↓
更新 Rules / Skills / Knowledge / Templates
   ↓
下次 AI 直接复用
   ↓
继续发现问题
```

形成：

```text
Experience
    ↓
Knowledge
    ↓
Pattern
    ↓
Skill / Rule
    ↓
Automation
    ↓
更高效的 AI Development
```

---

# 2. 六类内容分别沉淀什么

整个系统固定使用六个核心目录：

```text
rules/
skills/
agents/
knowledge/
templates/
scripts/
```

不要看到一个问题就随意创建文件。

首先判断：

> 这个信息未来到底是什么类型？

---

## 2.1 rules：长期必须遵守的规则

Rule 回答：

> “以后所有相关任务都应该怎么做？”

适合沉淀：

* 编码规范
* Git 规范
* 测试规范
* 安全规范
* AI 工作流程
* 跨项目通用约束

例如：

```text
不要提交 API Key
```

适合：

```text
rules/global/security.md
```

而不是 Knowledge。

---

## 2.2 skills：完成任务的方法

Skill 回答：

> “遇到这种任务，应该怎么完成？”

例如：

```text
如何进行 Bug 修复？
如何进行 React 项目重构？
如何排查 Webpack 构建问题？
如何进行依赖升级？
```

适合：

```text
skills/task/
skills/stack/
```

例如：

```text
skills/task/bug-fix/SKILL.md
skills/stack/react/SKILL.md
```

---

## 2.3 agents：角色和职责

Agent 回答：

> “这个角色应该负责什么？”

例如：

```text
Planner
Developer
Reviewer
Debugger
```

Agent 不应该重复 Skill 的具体内容。

例如：

```text
Reviewer
```

负责：

```text
检查代码
检查测试
检查风险
提出问题
```

具体如何进行 Review，可以由：

```text
skills/task/code-review/
```

提供。

---

## 2.4 knowledge：已经发生过的问题和经验

Knowledge 回答：

> “以前遇到过什么问题？最后是怎么解决的？”

例如：

```text
React + CRACO + react-pdf
Webpack 无法解析 private class
```

这类信息应该进入：

```text
knowledge/build/
```

Knowledge 的价值在于：

> 避免下一次重新花同样的时间排查。

---

## 2.5 templates：标准输出格式

Template 回答：

> “这类工作应该以什么格式记录？”

例如：

```text
Bug 报告
Task 计划
Code Review
AGENTS.md
```

Template 不负责解决问题，只负责统一结构。

---

## 2.6 scripts：可以自动执行的事情

Script 回答：

> “哪些事情不应该让 AI 每次手动做？”

例如：

```text
检测项目类型
执行测试
执行构建
检查代码
检查敏感信息
```

如果一个动作可以稳定自动化，优先考虑 Script。

---

# 3. 沉淀决策树

遇到新的经验时，按照下面的流程判断：

```text
                    新经验
                      │
                      ▼
             是否只发生过一次？
                 /          \
               是            否
               │             │
           暂时不沉淀       是否具有通用性？
                            /        \
                          否          是
                          │           │
                       Knowledge   继续判断
                                      │
                ┌─────────────────────┼─────────────────────┐
                │                     │                     │
                ▼                     ▼                     ▼
           长期必须遵守？        完成任务的方法？       标准输出格式？
                │                     │                     │
               是                    是                    是
                ↓                     ↓                     ↓
              Rule                 Skill                Template
                                     
                │
                ▼
           是否需要角色？
                │
               是
                ↓
              Agent

                │
                ▼
        是否可以自动执行？
                │
               是
                ↓
              Script
```

简单记忆：

```text
Rule      = 必须遵守
Skill     = 怎么做
Agent     = 谁来做
Knowledge = 遇到过什么
Template  = 怎么记录
Script    = 怎么自动做
```

---

# 4. 什么情况下必须沉淀

并不是所有问题都值得记录。

推荐满足以下任意条件时进行沉淀：

## 4.1 很可能再次发生

例如：

```text
Node 版本
Vue 版本
React 版本
Webpack
Babel
pnpm
Maven
Docker
```

经常遇到兼容性问题。

应该考虑沉淀。

---

## 4.2 排查过程比较复杂

例如一个问题需要：

```text
检查配置
→ 检查依赖
→ 检查编译器
→ 检查 Node
→ 检查 Loader
→ 修改配置
→ 验证
```

这种排查过程本身就有价值。

---

## 4.3 官方文档不容易直接解决

例如：

```text
多个工具组合之后出现的问题
```

典型：

```text
CRA
+
CRACO
+
Babel
+
Webpack
+
某个第三方依赖
```

官方文档可能分别解释每个组件，但不会解释你的组合环境。

这类问题特别适合 Knowledge。

---

## 4.4 可以减少未来 AI 的探索成本

如果记录以后可以让 AI 少执行：

```text
10 次搜索
```

甚至：

```text
30 分钟排查
```

就值得沉淀。

---

# 5. 什么情况下不要沉淀

以下内容通常不需要进入知识库：

## 5.1 一次性小问题

例如：

```text
某个变量拼写错误
```

通常不需要记录。

---

## 5.2 官方文档直接可查

例如：

```text
npm install xxx
```

如果官方文档已经非常清楚，没有必要复制一份。

---

## 5.3 没有验证过的猜测

禁止把：

```text
我猜可能是……
```

直接写进 Knowledge。

必须区分：

```text
事实
猜测
验证结果
```

---

## 5.4 临时 workaround

例如：

```text
临时关闭某个检查
临时修改 node_modules
临时删除缓存
```

除非验证后确认这是稳定解决方案，否则不要直接沉淀为正式经验。

可以记录为：

```text
排查过程
```

但必须标记：

```text
临时方案
未确认长期有效
```

---

# 6. Knowledge 标准格式

推荐所有故障类 Knowledge 使用统一格式。

文件：

```text
knowledge/<category>/<problem-name>.md
```

例如：

```text
knowledge/build/react-pdf-private-class.md
```

内容：

````markdown
# 问题标题

## 问题

描述问题。

## 环境

- OS:
- Node:
- Package Manager:
- Framework:
- Build Tool:
- 相关依赖：

## 现象

描述实际错误。

## 复现

描述如何触发。

## 排查过程

### 1. 检查 xxx

结果：

### 2. 检查 xxx

结果：

### 3. 检查 xxx

结果：

## 根因

确认后的根本原因。

## 解决方案

最终采用的解决方案。

## 验证

执行：

```bash
xxx
````

结果：

```text
PASS
```

## 备选方案

如果存在其他方案，记录在这里。

## 风险

说明方案可能带来的影响。

## 适用范围

说明哪些项目可以使用。

## 相关版本

记录关键版本。

## 最后验证时间

YYYY-MM-DD

````

---

# 7. Knowledge 最重要的原则：记录“为什么”

不要只记录：

```text
执行 xxx 命令即可解决。
````

应该记录：

```text
为什么这个命令有效？
```

例如：

错误：

```text
升级 Babel 即可解决。
```

正确：

```text
原因是当前构建链使用的 Babel Parser 不支持依赖中的 private class syntax。

升级 Babel 后 Parser 可以解析该语法，因此构建恢复。

但如果项目需要兼容旧版浏览器，还需要继续检查最终输出代码是否满足目标浏览器要求。
```

AI 真正需要的是：

```text
现象
→ 原因
→ 方案
→ 为什么
→ 限制
```

---

# 8. 从 Knowledge 升级为 Skill

一个 Knowledge 如果重复出现，可以进一步升级成 Skill。

例如：

第一次：

```text
Webpack 构建失败
```

记录：

```text
knowledge/build/webpack-build-failure.md
```

第二次：

```text
又遇到类似问题
```

发现有稳定排查套路：

```text
检查 Node
→ 检查依赖
→ 检查 Loader
→ 检查 Parser
→ 检查 Babel
→ 检查配置
→ 最小复现
```

可以建立：

```text
skills/task/troubleshooting/SKILL.md
```

形成：

```text
Knowledge
    ↓
发现规律
    ↓
形成通用方法
    ↓
Skill
```

---

# 9. 从 Skill 升级为 Rule

只有当某个原则变成：

> “以后所有项目都必须这样做。”

才应该升级成 Rule。

例如最初：

```text
某次 Bug 修复发现修改代码前应该先检查 git diff。
```

如果验证后发现这个原则适用于所有项目：

```text
修改代码前检查工作区状态
```

可以进入：

```text
rules/global/git.md
```

形成：

```text
经验
 ↓
验证
 ↓
通用原则
 ↓
Rule
```

---

# 10. 从 Skill 升级为 Script

如果一个 Skill 中存在稳定、重复、机械的步骤：

```text
执行 typecheck
执行 lint
执行 test
执行 build
```

应该考虑自动化。

例如：

```text
skills/task/feature-development/
```

中原来写：

```text
完成后执行：

npm run lint
npm test
npm run build
```

如果所有项目都可以标准化，就可以进一步建立：

```text
scripts/verify.sh
```

形成：

```text
人工流程
 ↓
稳定流程
 ↓
Skill
 ↓
自动化
 ↓
Script
```

---

# 11. 文档完善流程

以后增加任何文档，统一执行：

```text
1. 确定问题
2. 判断所属类型
3. 查找是否已有文档
4. 避免重复
5. 创建 / 修改文档
6. 实际验证
7. 更新相关索引
8. Review
```

---

# 12. 新增文档之前先搜索

禁止：

```text
想到一个问题
→
直接创建新文件
```

应该先搜索：

```text
rules/
skills/
knowledge/
templates/
agents/
```

确认是否已经存在：

```text
相关 Rule
相关 Skill
相关 Knowledge
```

如果已有内容：

```text
优先修改已有文档
```

而不是创建重复文档。

---

# 13. 文档重复处理

如果发现两个文档内容高度重复：

```text
A.md
B.md
```

不要继续增加第三份。

应该判断：

```text
A 和 B 是同一个问题？
        │
       是
        ↓
合并

A 和 B 是不同问题？
        │
       是
        ↓
明确边界
```

目标：

> 一个概念尽量只有一个权威来源。

---

# 14. 文档之间不要复制内容

例如：

```text
rules/global/security.md
```

已经定义：

```text
禁止提交 API Key
```

其他 Skill 不应该再次完整复制：

```text
禁止提交 API Key
禁止提交 Token
禁止提交 Password
...
```

而应该只引用原则：

```text
遵循 global security rules。
```

这样可以避免规则漂移。

---

# 15. 文档修改必须考虑影响范围

修改：

```text
rules/
```

可能影响所有项目。

修改：

```text
skills/stack/react/
```

可能影响所有 React 项目。

修改：

```text
project/AGENTS.md
```

通常只影响一个项目。

因此修改前应该判断：

```text
影响范围：

Global
Stack
Task
Project
Single Problem
```

影响越大，验证要求越高。

---

# 16. Rule 修改流程

修改 Global Rule 时：

```text
1. 为什么要修改？
2. 哪些项目受到影响？
3. 是否存在例外？
4. 是否会与现有 Rule 冲突？
5. 是否需要更新 Skill？
6. 是否需要更新 Template？
7. 是否需要更新项目 AGENTS.md？
```

Global Rule 不应该为了一个项目的特殊情况而修改。

如果只是项目特殊要求：

```text
放项目 AGENTS.md
```

---

# 17. Skill 修改流程

修改 Skill 时：

```text
1. 这个 Skill 解决什么问题？
2. 使用场景是什么？
3. 输入是什么？
4. 输出是什么？
5. 步骤是否清晰？
6. 是否包含验证？
7. 是否存在不必要的步骤？
8. 是否与其他 Skill 重复？
```

Skill 最重要的是：

```text
可执行
```

AI 看完应该知道：

```text
下一步做什么
```

而不是只知道：

```text
理论上应该怎么做
```

---

# 18. Agent 修改流程

修改 Agent 时：

```text
1. 明确角色
2. 明确职责
3. 明确输入
4. 明确输出
5. 明确禁止事项
6. 明确验收方式
```

避免多个 Agent 职责重叠。

例如：

```text
Planner
```

主要负责：

```text
分析 + 规划
```

而：

```text
Developer
```

主要负责：

```text
实现 + 验证
```

---

# 19. Template 修改流程

Template 修改时重点检查：

```text
是否足够通用？
是否过于复杂？
是否缺少关键字段？
是否已经被实际使用？
```

Template 不应该追求：

```text
字段越多越好
```

而应该追求：

```text
刚好覆盖工作需要
```

---

# 20. 文档质量标准

一个好的 AI 文档应该具备：

```text
明确
具体
可执行
可验证
可复用
边界清晰
```

避免：

```text
空泛
重复
过度抽象
大量废话
未经验证的结论
```

---

# 21. 推荐的文档写作结构

对于规则：

```text
目的
规则
应该做什么
不应该做什么
例外
```

对于 Skill：

```text
目标
适用场景
输入
流程
验证
失败处理
输出
```

对于 Knowledge：

```text
问题
环境
现象
复现
排查
根因
方案
验证
风险
```

对于 Agent：

```text
角色
职责
输入
工作流程
禁止事项
输出
验收
```

---

# 22. 每次实际开发后的沉淀流程

完成一个比较复杂的开发任务后，建议进行一次：

```text
Post Task Review
```

问自己：

```text
1. 这次遇到了什么新问题？
2. 有没有花大量时间排查的问题？
3. 有没有反复搜索的问题？
4. 有没有踩坑？
5. 有没有形成新的稳定方法？
6. 有没有发现现有 Rule 不合理？
7. 有没有 Skill 可以改进？
8. 有没有步骤可以自动化？
```

然后进行分类：

```text
问题经验
    ↓
Knowledge

稳定方法
    ↓
Skill

长期原则
    ↓
Rule

角色职责
    ↓
Agent

固定格式
    ↓
Template

机械步骤
    ↓
Script
```

---

# 23. 建议建立“沉淀候选区”

如果暂时无法判断是否值得沉淀，不要强行分类。

可以建立：

```text
knowledge/_inbox/
```

例如：

```text
knowledge/
├── _inbox/
│   ├── 2026-09-react-pdf.md
│   └── 2026-09-maven.md
│
├── frontend/
├── backend/
├── build/
├── dependency/
└── troubleshooting/
```

`_inbox` 是临时收集区。

周期性整理：

```text
_inbox
   ↓
Review
   ↓
删除 / 合并 / Knowledge / Skill / Rule
```

不要让 `_inbox` 永久变成垃圾场。

---

# 24. 建议的沉淀周期

不需要每天整理整个系统。

推荐：

## 每次任务

只做：

```text
发现高价值经验
→ 简单记录
```

## 每周

做一次：

```text
Knowledge Review
```

检查：

```text
新增问题
重复问题
值得升级的经验
过时内容
```

## 每月

做一次：

```text
AI Engineering Review
```

检查：

```text
Rules
Skills
Agents
Knowledge
Templates
Scripts
```

重点删除：

```text
过时
重复
无效
未经验证
```

---

# 25. 版本和时间记录

涉及技术版本的问题，应记录版本。

例如：

```markdown
## 环境

- Node: 22.23.2
- npm: 10.x
- React: 18.x
- CRACO: x.x
- Webpack: x.x
```

如果方案可能随版本变化，必须说明：

```markdown
> 本方案针对上述版本验证。
> 升级相关依赖后需要重新验证。
```

Knowledge 不是永久真理。

它是：

> 在特定环境下经过验证的经验。

---

# 26. 已过时知识的处理

技术知识会过期。

发现 Knowledge 已经不适用时：

不要直接删除历史。

可以增加：

```markdown
## 状态

Deprecated

## 原因

xxx 版本之后已经不再适用。

## 替代方案

xxx
```

如果完全没有保留价值，再删除。

---

# 27. 如何判断一个 Knowledge 是否应该升级

可以使用下面的标准：

```text
                    Knowledge
                         │
                         ▼
                是否重复发生？
                    /        \
                  否          是
                  │            │
                保留         是否可以标准化？
                              /      \
                            否        是
                            │          │
                         Knowledge   Skill
                                         │
                                         ▼
                                  是否所有项目通用？
                                    /        \
                                  否          是
                                  │            │
                               Stack Skill    Rule
```

注意：

不是所有 Knowledge 都应该升级。

知识库本身就是有价值的。

---

# 28. AI 使用这些文档时的原则

AI 不应该默认读取整个仓库。

推荐：

```text
当前项目
    ↓
项目 AGENTS.md
    ↓
判断任务
    ↓
加载 Task Skill
    ↓
加载 Stack Skill
    ↓
检索相关 Knowledge
    ↓
执行
    ↓
验证
```

例如：

```text
React 项目
+
构建失败
```

加载：

```text
Global Rules
+
Project AGENTS.md
+
bug-fix
+
troubleshooting
+
react
+
相关 build Knowledge
```

而不是加载：

```text
Java Skill
Vue Skill
所有 Knowledge
所有 Agent
```

---

# 29. AI 完成任务后的沉淀判断

AI 在任务结束时可以自动进行：

```text
Knowledge Candidate Review
```

输出：

```text
本次任务是否产生新的可复用经验？

[ ] 否

[ ] 是，建议 Knowledge

[ ] 是，建议更新已有 Knowledge

[ ] 是，建议升级 Skill

[ ] 是，建议更新 Rule

[ ] 是，建议增加 Script
```

但 AI 不应该未经验证自动把经验提升成 Global Rule。

---

# 30. 推荐的最终工作闭环

整个系统最终应该形成：

```text
                  ┌──────────────┐
                  │  实际开发任务  │
                  └──────┬───────┘
                         ↓
                  ┌──────────────┐
                  │   AI 执行     │
                  └──────┬───────┘
                         ↓
                  ┌──────────────┐
                  │    验证       │
                  └──────┬───────┘
                         ↓
                  ┌──────────────┐
                  │  发现新经验   │
                  └──────┬───────┘
                         ↓
                  ┌──────────────┐
                  │   分类判断    │
                  └──────┬───────┘
                         ↓
        ┌────────────────┼────────────────┐
        ↓                ↓                ↓
    Knowledge          Skill            Rule
        │                │                │
        └────────────────┼────────────────┘
                         ↓
                  ┌──────────────┐
                  │   自动化      │
                  │ Scripts/Hooks │
                  └──────┬───────┘
                         ↓
                  下一次开发任务
```

---

# 31. 最重要的几个原则

## 原则 1：先解决，再沉淀

不要为了写文档而写文档。

```text
真实问题
→
真实解决
→
真实验证
→
再沉淀
```

---

## 原则 2：经验优先进入 Knowledge

不要第一次遇到问题就修改 Global Rule。

优先：

```text
Knowledge
```

经过多次验证之后，再考虑：

```text
Skill
```

最终确定为长期通用原则，才考虑：

```text
Rule
```

---

## 原则 3：不要重复

新增任何文档之前：

```text
Search First
```

先查：

```text
有没有类似内容？
```

---

## 原则 4：不要把猜测当知识

必须区分：

```text
猜测
事实
验证结果
```

没有验证的内容必须明确标记。

---

## 原则 5：让 AI 获得正确上下文

目标不是：

```text
让 AI 知道所有东西
```

而是：

```text
让 AI 在正确的时候获得正确的信息。
```

---

## 原则 6：能自动化就自动化

重复执行三次以上的机械步骤，就应该考虑：

```text
Script
Hook
Automation
```

---

## 原则 7：定期删除

AI Engineering System 不是“垃圾场”。

持续删除：

```text
重复内容
过时内容
无效经验
未经验证内容
```

和新增同样重要。

---

# 32. 最终判断口诀

遇到新东西时，只问六个问题：

```text
这是必须遵守的吗？
    → Rule

这是完成任务的方法吗？
    → Skill

这是一个角色的职责吗？
    → Agent

这是以前踩过的坑吗？
    → Knowledge

这是固定的输出格式吗？
    → Template

这是可以自动执行的吗？
    → Script
```

如果都不是：

```text
暂时不要沉淀。
```

---

# 33. 建设目标

最终希望形成：

```text
第一次遇到问题
    ↓
解决问题
    ↓
记录经验

第二次遇到类似问题
    ↓
AI 查询 Knowledge
    ↓
快速解决

问题不断重复
    ↓
形成 Skill

经验经过验证
    ↓
形成 Rule

重复步骤越来越多
    ↓
形成 Script / Hook

最终
    ↓
AI 不只是帮你写代码
    ↓
而是在不断学习你的工程方法
    ↓
形成个人 / 团队 AI Engineering System
```

最终目标不是：

> **让文档越来越多。**

而是：

> **让相同的问题越来越少重复思考，让 AI 每解决一个高价值问题，下一次都能更快、更稳定地完成。**
