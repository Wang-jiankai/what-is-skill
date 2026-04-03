# 01 | Skill 的多种含义

## 🎯 学习目标

- 理解 "Skill" 在 AI 领域的不同含义
- 分清 Claude Code Skill 与 Agent Skills 开放标准
- 避免概念混淆，精准沟通

---

## ⚠️ Skill 不是只有一个意思

"Skill" 是 AI 领域最容易混淆的词之一。同一个词，在不同语境下指的不是同一个东西。

| 语境 | 含义 | 格式 | 生态 |
|------|------|------|------|
| Claude Code 内置 Skill | CLI 内置的专门化子代理 | 代码实现，CLI 内置 | Claude Code 官方维护 |
| 自定义斜杠命令 | 用户自己封装的快捷命令 | `commands.json` | 用户自行维护 |
| Plugin Skill | 插件中封装的子代理 | 插件代码 | 插件开发者维护 |
| **Agent Skills（开放标准）** | **把领域 SOP 结构化打包** | **SKILL.md 文件** | **agentskills.io 开放生态** |

> **本仓库同时覆盖 Claude Code Skill 机制和 Agent Skills 开放标准**，让你既能用好 Claude Code 今天提供的 skill 能力，又能掌握跨平台的标准规范。

---

## Claude Code Skill 是什么？

Claude Code 的 Skill 指的是：**通过 `/<name>` 斜杠命令调用的专门化子代理（subagent）**。

Claude Code 内置了几个 Skill：

| Skill | 触发命令 | 功能 |
|-------|---------|------|
| ask | `/ask` | 问关于代码库的问题 |
| search | `/search` | 在代码库中搜索 |
| loop | `/loop` | 设置定时循环任务 |
| simplify | `/simplify` | 简化代码 |
| claude-api | `/claude-api` | 获取 Claude API 使用指导 |
| update-config | `/update-config` | 配置 Claude Code |

这些 Skill 本质上是一个专门的子 agent，当你对它说话时，它会接管对话、执行特定任务，然后返回结果。

---

## 自定义斜杠命令是什么？

除了内置 Skill，Claude Code 还支持**自定义斜杠命令**，通过 `commands.json` 文件配置：

```json
[
  {
    "name": "my-cmd",
    "description": "执行某个常用操作",
    "prompt": "你是一个XX专家，当用户说'my-cmd'时，执行以下操作..."
  }
]
```

用户可以把自己的常用 SOP 封装成斜杠命令，在任何对话中随时调用。

---

## Plugin Skill 是什么？

Claude Code 的插件（Plugin）可以自带 Skill，封装插件自己的能力。Plugin Skill 属于 Plugin 开发的一部分，本质上是一个受 Claude Code 管理的子 agent。

Plugin Skill 可以：
- 定义在插件的 `skills/` 目录下
- 被 Claude Code 自动发现和加载
- 调用插件提供的工具

---

## Agent Skills 开放标准是什么？

这是 agentskills.io 定义的跨平台标准，核心是一个 **SKILL.md 文件**：

```yaml
---
name: my-agent-skill
description: 当用户说...时触发
---

# My Agent Skill

## When to Use
## Steps
## Output Format
```

**关键区别：**
- Claude Code Skill：Claude Code 专有的代码实现
- Agent Skills：跨平台的开放标准，不绑定任何特定工具

---

## 为什么两套机制要同时学？

| 机制 | 优势 | 劣势 |
|------|------|------|
| Claude Code Skill | 今天就能用，原生集成 | 绑定 Claude Code |
| Agent Skills 标准 | 跨平台，可移植 | 生态还在建设中 |

**最佳实践：** 用 Claude Code Skill 解决今天的实际问题，用 Agent Skills 标准为未来布局。

---

## 📝 自我检测

- [ ] 能说清楚 Claude Code Skill 和 Agent Skills 的区别吗？
- [ ] 知道什么时候用自定义斜杠命令，什么时候用 Plugin Skill 吗？

继续学习：[02 - Claude Code 内置 Skill 深度用法](./02-builtin-skills-deep-dive.md)
