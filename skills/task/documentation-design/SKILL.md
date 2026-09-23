---
name: documentation-design
description: 软件开发文档体系的设计与维护：建立 README、架构、开发指南、API、部署文档，保证文档对人与 AI 都有用、与代码一致、可持续演进
---

# Documentation Design Skill

## 1. Purpose

本 Skill 用于软件项目开发文档的设计、创建、完善、重构和维护。

目标不是生成大量 Markdown，而是建立：

* 对开发人员有用
* 对 AI 有用
* 与代码保持一致
* 容易维护
* 可以持续演进

的软件开发文档体系。

---

## 2. When to Use

以下任务应考虑使用本 Skill：

* 新项目建立开发文档体系
* 为已有项目补充开发文档
* 重构混乱的项目文档
* 设计 README
* 设计架构文档
* 设计开发指南
* 设计 API 文档
* 设计部署文档
* 设计故障排查文档
* 设计贡献指南
* 设计项目 AI 上下文文档
* 检查文档与代码是否一致
* 根据开发过程中的经验持续完善文档

以下情况不应强制使用：

* 简单修改一个 README 拼写
* 修改单个配置说明
* 临时记录一次不会复用的信息
* 纯产品需求文档
* 与软件开发无关的普通文档

---

# 3. Core Principles

## 3.1 Documentation follows the project

先理解项目，再设计文档。

禁止在没有了解项目结构、技术栈和实际开发流程的情况下直接生成完整文档体系。

至少确认：

* 项目类型
* 技术栈
* 项目结构
* 构建工具
* 包管理器
* 开发命令
* 测试方式
* 构建方式
* 部署方式
* 主要模块
* 已有文档

---

## 3.2 Documentation should answer real questions

每份文档都应该明确回答开发人员的问题。

例如：

### README

回答：

> 这个项目是什么？如何快速运行？

### Architecture

回答：

> 项目由什么组成？模块如何协作？

### Development

回答：

> 我应该如何开发？

### API

回答：

> 如何调用系统接口？

### Deployment

回答：

> 如何构建和部署？

### Troubleshooting

回答：

> 出问题时如何定位？

如果无法明确说明文档解决什么问题，应重新考虑是否需要创建。

---

## 3.3 Prefer fewer useful documents

默认优先使用少量核心文档。

推荐基础集合：

```text
README.md
AGENTS.md
docs/
├── architecture.md
├── development.md
├── deployment.md
└── troubleshooting.md
```

不要为了“完整”创建大量文档。

只有当某类内容足够复杂、稳定并且具有独立维护价值时，才拆分独立文档。

---

# 4. Documentation Layers

项目文档按照作用分层。

## Layer 1: Project Entry

```text
README.md
```

负责：

* 项目是什么
* 解决什么问题
* 技术栈
* 快速开始
* 常用命令
* 文档入口

README 不应该承载所有详细知识。

---

## Layer 2: AI / Development Context

```text
AGENTS.md
```

负责：

* AI 开发规则
* 项目结构
* 技术约束
* 开发命令
* 测试命令
* 架构边界
* 修改代码时的注意事项
* Definition of Done

AGENTS.md 是 AI 工作上下文，不应该变成项目百科全书。

---

## Layer 3: Technical Documentation

```text
docs/
├── architecture.md
├── development.md
├── api.md
├── deployment.md
└── troubleshooting.md
```

负责具体技术知识。

---

## Layer 4: Knowledge / Experience

项目长期产生的问题和经验，应根据稳定程度进入：

```text
knowledge/
```

或团队共享：

```text
learnings/
```

不要把所有临时问题直接写进架构文档。

---

# 5. Documentation Design Workflow

执行以下流程：

```text
Understand
    ↓
Inventory
    ↓
Classify
    ↓
Design
    ↓
Write
    ↓
Verify
    ↓
Integrate
    ↓
Maintain
```

---

# 6. Phase 1 — Understand

先分析项目。

至少检查：

```text
README
AGENTS.md
package.json / pom.xml / build.gradle
配置文件
源码目录
测试目录
构建脚本
CI/CD
部署配置
现有 docs
```

根据项目类型执行相应命令。

例如：

```bash
find . -maxdepth 2 -type f | sort
```

Node / Frontend：

```bash
cat package.json
```

Java：

```bash
find . -maxdepth 2 -name "pom.xml" -o -name "build.gradle"
```

---

# 7. Phase 2 — Inventory

建立项目文档现状。

检查：

```text
已有文档
缺失文档
过时文档
重复文档
与代码不一致的文档
```

不要直接创建新文档。

先判断现有文档是否可以：

* 修改
* 合并
* 拆分
* 删除
* 保留

---

# 8. Phase 3 — Classify

将信息分类。

## Project

项目是什么。

## Architecture

系统如何组织。

## Development

如何开发。

## API

如何调用。

## Deployment

如何部署。

## Troubleshooting

如何解决问题。

## Rules

必须遵守什么。

## Knowledge

过去遇到过什么问题。

## Task

某个具体任务如何执行。

---

# 9. Phase 4 — Design

设计文档结构时遵循：

```text
用户问题
    ↓
文档
    ↓
章节
    ↓
具体答案
```

而不是：

```text
技术名词
    ↓
堆砌知识
```

每份文档创建之前明确：

```text
Document:
Purpose:
Audience:
When to read:
Source of truth:
Dependencies:
Maintenance owner:
```

---

# 10. Document Source of Truth

文档必须尽可能明确事实来源。

例如：

```text
开发命令
→ package.json scripts

Java 依赖
→ pom.xml

环境变量
→ .env.example / 配置文件

API
→ Controller / OpenAPI / Schema

项目结构
→ 实际源码目录

部署
→ Dockerfile / CI / deployment scripts
```

不要凭经验猜测项目行为。

---

# 11. Phase 5 — Write

写文档时：

### 优先事实

```text
实际命令
实际目录
实际配置
实际 API
实际依赖
实际流程
```

### 明确区分

```text
事实
约定
建议
限制
历史原因
TODO
```

不要把“建议”写成“项目事实”。

---

# 12. README Design

README 默认结构：

```markdown
# Project Name

## Overview

## Features

## Tech Stack

## Requirements

## Quick Start

## Development

## Build

## Test

## Project Structure

## Documentation

## Contributing
```

根据项目实际情况裁剪。

README 应该让新开发人员在最短时间内：

```text
理解项目
    ↓
安装依赖
    ↓
启动项目
    ↓
开始开发
```

---

# 13. Architecture Documentation

架构文档重点描述：

```text
系统边界
模块划分
模块职责
模块依赖
数据流
核心业务流程
关键技术决策
约束
```

推荐：

```markdown
# Architecture

## Overview

## System Context

## Module Structure

## Module Responsibilities

## Data Flow

## Key Flows

## Dependency Rules

## Important Constraints

## Architecture Decisions
```

避免逐文件解释源码。

---

# 14. Development Documentation

开发文档应该回答：

```text
如何安装
如何启动
如何开发
如何测试
如何构建
如何调试
如何提交代码
```

推荐：

```markdown
# Development Guide

## Requirements

## Installation

## Environment

## Start

## Development Commands

## Testing

## Build

## Debugging

## Code Conventions

## Git Workflow
```

命令必须优先从项目实际配置中确认。

---

# 15. API Documentation

API 文档应该优先描述：

```text
Endpoint
Method
Authentication
Request
Response
Error
Example
```

不要重复粘贴大量实现代码。

如果项目已有 OpenAPI / Swagger：

> 优先把 OpenAPI 作为 API 的事实来源，Markdown 只负责补充使用场景和说明。

---

# 16. Deployment Documentation

部署文档至少说明：

```text
环境要求
环境变量
构建
部署
启动
停止
健康检查
日志
回滚
```

必须区分：

```text
开发环境
测试环境
生产环境
```

不能把不同环境的配置混在一起。

---

# 17. Troubleshooting Documentation

故障文档采用：

```text
Problem
Symptoms
Cause
Diagnosis
Solution
Verification
Prevention
```

例如：

```markdown
## Problem

项目启动失败。

## Symptoms

...

## Cause

...

## Diagnosis

...

## Solution

...

## Verification

...

## Prevention

...
```

重点记录：

> 为什么发生 + 如何确认 + 如何解决。

而不仅仅记录最终命令。

---

# 18. Documentation and Code Verification

文档完成后必须进行验证。

至少检查：

### Commands

```bash
npm run ...
pnpm ...
mvn ...
./gradlew ...
```

是否真实存在。

### Paths

文档中的目录和文件是否存在。

### Configuration

环境变量和配置名称是否真实存在。

### Dependencies

文档中的技术栈是否与项目实际依赖一致。

### API

接口名称、路径和参数是否与代码一致。

---

# 19. Stale Documentation Detection

修改代码后，如果影响：

```text
目录结构
API
配置
命令
依赖
部署
架构
```

必须检查相关文档。

建立：

```text
Code Change
    ↓
Impact Analysis
    ↓
Documentation Check
    ↓
Update Documentation
```

文档更新不能作为完全独立于代码的工作。

---

# 20. Documentation Change Rules

### 新功能

检查：

```text
README
Architecture
API
Development
```

是否需要更新。

### Bug Fix

如果产生可复用经验：

```text
knowledge/
```

如果是稳定规则：

```text
rules/
```

如果形成标准操作方法：

```text
skills/
```

### 重构

检查：

```text
Architecture
Project Structure
Development
```

### 依赖升级

检查：

```text
Tech Stack
Development
Compatibility
Troubleshooting
```

---

# 21. Knowledge Promotion

文档和知识应该形成演进关系：

```text
一次问题
    ↓
Knowledge
    ↓
重复出现
    ↓
稳定解决方法
    ↓
Skill
    ↓
跨项目复用
    ↓
Team Skill
```

如果经验变成强制性团队规范：

```text
Knowledge
    ↓
Rule
```

不要一开始就把所有问题写成 Rule。

---

# 22. AI-Friendly Documentation

文档应便于 AI 检索和理解。

优先：

```text
明确标题
短章节
明确术语
明确命令
明确条件
明确示例
明确限制
```

避免：

```text
超长段落
重复描述
模糊表述
没有上下文的代码片段
过时命令
隐藏关键约束
```

推荐：

```markdown
## When to Use

## Preconditions

## Procedure

## Verification

## Common Problems

## Constraints
```

---

# 23. Documentation Quality Checklist

完成后检查：

* [ ] 文档有明确目的
* [ ] 面向对象明确
* [ ] 内容来自项目实际情况
* [ ] 没有明显重复
* [ ] 命令经过验证
* [ ] 路径经过验证
* [ ] 配置名称经过验证
* [ ] API 与代码一致
* [ ] 没有把推测写成事实
* [ ] 没有不必要的大段代码
* [ ] README 保持简洁
* [ ] 详细内容放在 docs
* [ ] 可复用经验进入 knowledge
* [ ] 稳定规则进入 rules
* [ ] 稳定工作方法进入 skills

---

# 24. Definition of Done

一个开发文档任务只有同时满足以下条件才算完成：

```text
1. 文档结构合理
2. 内容基于项目事实
3. 关键命令已经验证
4. 关键路径已经验证
5. 与当前代码保持一致
6. 没有明显重复
7. 文档放置位置正确
8. 明确后续维护方式
```

---

# 25. Output Strategy

AI 执行文档任务时，不要一次性生成大量文档。

优先：

```text
分析
 ↓
提出文档结构
 ↓
确认/修正
 ↓
创建核心文档
 ↓
验证
 ↓
补充文档
```

对于大型项目：

```text
Phase 1
README + AGENTS

Phase 2
Architecture + Development

Phase 3
API + Deployment

Phase 4
Troubleshooting + Knowledge

Phase 5
Consistency Review
```

---

# 26. Final Principle

文档体系应该遵循：

```text
少而有用
事实优先
代码为源
持续验证
经验沉淀
按需加载
```

最终目标：

> 让一个新的开发人员能够快速理解项目，让 AI 能够快速获得正确上下文，并让文档随着代码一起持续演进。
