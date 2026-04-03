# 01 | 练习：Skill 的多种含义

## 🎯 练习目标

- 理解 Skill 在 AI 领域的不同含义
- 能区分 Claude Code Skill 和 Agent Skills 开放标准
- 理解为什么一个词指代多个不同概念

---

## 📋 练习要求

### 基础任务（必做）

**1. 填写下表，判断每个场景指的是哪种 Skill：**

| 场景 | 哪种 Skill？ |
|------|-------------|
| 用户在 Claude Code 中输入 `/ask "这个函数干啥的"` | |
| 用户配置了 `commands.json`，定义了一个 `/deploy` 命令 | |
| 一个插件的 `skills/` 目录下有 `SKILL.md` 文件 | |
| agentskills.io 上发布的 `SKILL.md` 文件 | |
| Claude Code 内置的 `/loop` 定时任务 | |
| 用户在 `~/.claude/commands.json` 中定义的斜杠命令 | |

**2. 判断对错：**

- [ ] Claude Code 的 `/ask` 和 agentskills.io 的 Skill 是同一个东西
- [ ] 自定义斜杠命令和 Plugin Skill 本质上都是 prompt 封装
- [ ] Agent Skills 标准可以被任何采纳该标准的工具使用
- [ ] Claude Code Skill 只能在 Claude Code 中使用

**3. 思考题：**

为什么 Anthropic 没有把所有 Skill 机制统一成一种？

### 进阶任务（选做）

**调研：**
1. Claude Code 官方文档中 Skill 相关的内容在哪里？
2. agentskills.io 上有多少个公开 Skill？
3. 两者有没有互相引用或推荐对方？

---

## 💡 提示

- 本练习对应的概念文章：[`concepts/01-skill-meanings.md`](../concepts/01-skill-meanings.md)
- 参考答案：[`references/01-skill-meanings-solution.md`](../references/01-skill-meanings-solution.md)
