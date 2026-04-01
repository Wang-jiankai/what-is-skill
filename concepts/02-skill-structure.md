# 02 | SKILL.md 的结构

## 🎯 学习目标

- 掌握 SKILL.md 的标准结构
- 理解 YAML 元数据的写法
- 理解 Markdown 正文的层次结构

---

## 📖 概念讲解

### SKILL.md 的两个部分

SKILL.md 文件分两部分：

```
---                          ← 分隔线
name: my-skill              ← YAML 元数据
description: 简短描述
---
# My Skill                  ← Markdown 正文

## When to Use
## Steps
## Output Format
```

**YAML 部分**（`---` 之间）：机器可读，元数据
**Markdown 部分**：人类可读，核心内容

### YAML 元数据

```yaml
---
name: code-review           # 必须：Skill 名称（英文，snake-case）
description: 团队代码审查 SOP。当用户说 "review this PR" 或 "审查代码" 时触发。
# name 和 description 是 Level 1 内容，始终加载
---
```

**YAML 字段规范**：

| 字段 | 必须 | 说明 |
|------|------|------|
| `name` | ✅ | Skill 名称，英文、snake-case |
| `description` | ✅ | 一句话描述，建议包含触发关键词 |

### Markdown 正文结构

一个高质量的 SKILL.md 正文，通常包含以下章节：

```markdown
# Skill 名称

## When to Use（何时使用）
  - 触发条件
  - 不适用场景

## Prerequisites（前置要求）
  - 需要什么输入
  - 环境要求

## Steps（操作步骤）
  1. 第一步
  2. 第二步
  3. 第三步

## Output Format（输出格式）
  - 应该输出什么
  - 格式规范

## Examples（示例）
  ```示例代码
  ```

## Edge Cases（边界情况）
  - 如何处理异常
  - 特殊场景
```

### 核心原则：结构化，不模糊

**❌ 低质量描述（模糊）：**
> "审查代码，检查有没有问题，注意代码质量。"

**✅ 高质量描述（结构化）：**
> "按以下顺序审查代码：1. 安全性 → 2. 逻辑 → 3. 性能 → 4. 风格。每项必须给出明确结论。"

---

## 📝 章节回顾

**记住：**

1. **YAML 元数据 = Level 1**：始终加载，name + description 是 AI 判断是否触发的唯一依据
2. **Markdown 正文 = Level 2 + 3**：核心 Instructions，结构化、不模糊
3. **好 Skill 的标准**：AI 看完后，每次执行路径一致

---

## ❓ 自我检测

- [ ] 能写出规范格式的 YAML 元数据吗？
- [ ] 能判断一个 SKILL.md 正文是结构化还是模糊的吗？

继续学习：[03 - 写好 Instructions](./03-writing-instructions.md)
