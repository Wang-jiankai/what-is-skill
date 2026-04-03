# 09 | 练习：写好 Instructions

## 🎯 练习目标

- 掌握把专家经验转成结构化 Instructions 的方法
- 能写清楚触发条件和输出规范
- 能识别并修正模糊的 Instructions

---

## 📋 练习要求

### 基础任务（必做）

**1. 把以下专家经验转成结构化 Instructions：**

> 专家说："发布 npm 包之前，要检查 package.json 的 version 字段是否正确，运行 tests 确保测试通过，然后用 npm publish 发布。记得检查 isPublishable 字段。"

转成 Instructions：

```markdown
## Steps

1. [第一步]
2. [第二步]
3. [第三步]
```

**2. 找出以下 Instructions 的问题并修正：**

❌ 原文（问题 Instructions）：
```markdown
## Output Format
给出分析结果。
```

✅ 修正（规范 Instructions）：
```markdown
## Output Format
[你的修正]
```

**3. 为以下场景写触发条件和 Edge Cases：**

场景：技术方案评审 Skill

- 触发条件应该包含哪些关键词？
- 什么情况下**不应该**触发这个 Skill？
- 有哪些 Edge Cases 需要处理？

### 进阶任务（选做）

**找一段你工作中的 SOP（可以是自己写的、团队的 wiki、或公司的规范文档），把它转成 SKILL.md 的 Instructions 部分。**

---

## 💡 提示

- 本练习对应的概念文章：[`concepts/09-writing-instructions.md`](../concepts/09-writing-instructions.md)
- 参考答案：[`references/09-writing-instructions-solution.md`](../references/09-writing-instructions-solution.md)
