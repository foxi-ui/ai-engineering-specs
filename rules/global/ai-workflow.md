# AI Development Workflow

## 总原则

AI 不应该直接从需求跳到代码。

所有中大型任务遵循：

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
Summary
```

---

# 1. Understand

首先理解任务。

需要明确：

- 用户要解决什么问题
- 期望行为是什么
- 当前行为是什么
- 成功标准是什么
- 是否存在约束
- 是否存在兼容性要求

如果需求存在明显歧义，不要擅自扩大需求。

---

# 2. Explore

修改代码前搜索项目。

至少检查：

- 项目结构
- package.json / pom.xml
- 入口
- 相关模块
- 调用方
- 被调用方
- 类型定义
- 测试
- 配置

优先搜索已有实现。

---

# 3. Plan

对于非简单任务，先给出计划。

计划应该包含：

```text
目标
修改文件
修改原因
实现方式
风险
验证方式
```

不要为了简单任务产生巨大计划。

---

# 4. Implement

按照计划实现。

原则：

- 最小修改
- 优先复用
- 保持架构
- 保持 API
- 不做无关重构

如果实施过程中发现计划不成立：

```text
停止
↓
重新分析
↓
更新计划
↓
继续
```

不要强行按照错误计划继续。

---

# 5. Verify

代码修改后必须验证。

优先：

```text
TypeCheck
↓
Lint
↓
Unit Test
↓
Integration Test
↓
Build
```

根据项目实际情况选择。

---

# 6. Review

验证通过后进行自我 Review。

检查：

### Correctness

是否真正解决问题？

### Regression

是否破坏已有功能？

### Compatibility

是否破坏旧环境？

### Security

是否引入安全问题？

### Maintainability

是否容易维护？

### Scope

是否修改了无关代码？

---

# 7. Summary

最终报告：

```text
## Changes

修改了什么

## Files

修改了哪些文件

## Verification

TypeCheck:
Lint:
Test:
Build:

## Risks

存在什么风险

## Notes

其他需要人工关注的问题
```

---

# 简单任务

例如：

- 修改一个变量名
- 增加一个简单配置
- 修复一个 typo

可以简化：

```text
Understand
→ Implement
→ Verify
→ Summary
```

---

# 禁止行为

禁止：

- 没看代码直接修改
- 没验证就宣布完成
- 为了测试通过修改测试绕过问题
- 发现问题后擅自扩大需求
- 无理由大规模重构
- 使用猜测代替实际检查

---

# 人机边界

AI 可以：

- 分析
- 搜索
- 修改代码
- 编写测试
- 执行验证
- Review

人负责：

- 产品目标
- 架构重大决策
- 数据删除
- 生产环境操作
- 高风险安全决策
- 最终合并