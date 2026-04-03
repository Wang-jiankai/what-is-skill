# 07 | 练习：SKILL.md 格式与结构

## 🎯 练习目标

- 掌握 SKILL.md 的标准结构
- 能判断一个 SKILL.md 是否规范
- 能写出规范的 YAML 元数据

---

## 📋 练习要求

### 基础任务（必做）

**1. 分析以下 YAML 元数据，指出问题：**

```yaml
---
name: review
description: 代码审查
---
```

问题在哪里？应该如何修改？

**2. 为以下场景写规范的 YAML 元数据：**

场景：Skill 名称是 `db-migration`，用于数据库变更 SOP。当用户说 "migration"、"数据库变更"、"alter table" 时触发。

```yaml
---
# 在此填写
name:
description:
---
```

**3. 判断以下 SKILL.md 结构是否规范：**

```markdown
# My Skill

这个 Skill 用于审查代码。

## Steps
1. 检查安全性
2. 检查逻辑
3. 检查性能

有问题吗？应该如何组织？
```

### 进阶任务（选做）

**为一个"日志分析"场景，写出完整的 SKILL.md 结构**（只写大纲，不写详细内容）：

包含：YAML 元数据、When to Use、Prerequisites、Steps（3步以上）、Output Format、Edge Cases。

---

## 💡 提示

- 本练习对应的概念文章：[`concepts/07-skillmd-format.md`](../concepts/07-skillmd-format.md)
- 参考答案：[`references/07-skillmd-format-solution.md`](../references/07-skillmd-format-solution.md)
