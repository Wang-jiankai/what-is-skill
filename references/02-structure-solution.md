# 02 | 参考答案：SKILL.md 结构

## 📋 基础任务参考答案

### 任务 1：YAML 元数据分析

```yaml
---
name: review
description: 代码审查
---
```

**问题：**

1. `name: review` 太通用，容易和其他 Skill 冲突
2. `description: 代码审查` 太模糊，AI 无法判断何时触发

**修正：**

```yaml
---
name: code-review
description: 团队代码审查 SOP。当用户说 "review this PR"、"审查代码"、"代码审查"、"review code" 时触发。
---
```

### 任务 2：规范 YAML 元数据

```yaml
---
name: db-migration
description: 数据库变更 SOP。当用户说 "migration"、"数据库变更"、"alter table"、"schema change" 时触发。
---
```

### 任务 3：结构规范判断

原文：
```markdown
# My Skill

这个 Skill 用于审查代码。

## Steps
1. 检查安全性
2. 检查逻辑
3. 检查性能

有问题吗？应该如何组织？
```

**问题：**
1. 缺少 YAML 元数据
2. 缺少 `When to Use`（何时触发）
3. 步骤太笼统（"检查安全性"是什么意思？）
4. 缺少 `Output Format`

**规范结构：**

```markdown
---
name: code-review
description: 团队代码审查 SOP...
---

# Code Review SOP

## When to Use
当用户要求审查代码或 review PR 时使用。

## Prerequisites
- 已获取需要审查的代码

## Steps

### 1. Security
检查：SQL 注入、XSS、硬编码密钥

### 2. Correctness
检查：空指针、边界条件、异常处理

### 3. Performance
检查：N+1、循环优化、索引

## Output Format
必须包含：
- 🔴 Critical Issues（如有）
- 🟡 Suggestions（如有）
- ✅ Summary（总评）
```
