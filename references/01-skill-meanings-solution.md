# 01 | 参考答案：Skill 的多种含义

## 📋 基础任务参考答案

### 任务 1：填写下表

| 场景 | 哪种 Skill？ |
|------|-------------|
| 用户在 Claude Code 中输入 `/ask "这个函数干啥的"` | Claude Code 内置 Skill |
| 用户配置了 `commands.json`，定义了一个 `/deploy` 命令 | 自定义斜杠命令 |
| 一个插件的 `skills/` 目录下有 `SKILL.md` 文件 | Plugin Skill |
| agentskills.io 上发布的 `SKILL.md` 文件 | Agent Skills 开放标准 |
| Claude Code 内置的 `/loop` 定时任务 | Claude Code 内置 Skill |
| 用户在 `~/.claude/commands.json` 中定义的斜杠命令 | 自定义斜杠命令 |

### 任务 2：判断对错

- [x] Claude Code 的 `/ask` 和 agentskills.io 的 Skill 是同一个东西 — **错**：不是同一个东西
- [x] 自定义斜杠命令和 Plugin Skill 本质上都是 prompt 封装 — **对**：都是 prompt 指令
- [x] Agent Skills 标准可以被任何采纳该标准的工具使用 — **对**：这是开放标准的优势
- [x] Claude Code Skill 只能在 Claude Code 中使用 — **对**：这是 Claude Code 专有的

### 任务 3：思考题答案

Anthropic 没有统一 Skill 机制的原因：
- **历史演进**：Claude Code Skill 先出现，Agent Skills 是后来定义的开放标准
- **使用场景不同**：Claude Code Skill 是 CLI 内的子代理，Agent Skills 是跨平台的知识打包格式
- **复杂度不同**：Claude Code Skill 可以调用工具，Agent Skills 主要是 prompt 指令

---

## 继续学习

→ 下一章：[02 - 内置 Skill 深度用法](../concepts/02-builtin-skills-deep-dive.md)
