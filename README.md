# ⚡ What is Skill?

> **"Skill" 是 AI 时代的设计方法论——把专家经验打包成可复用的 SOP。** 本仓库探索 Skill 的概念与实践，教你如何把人类专家的领域经验结构化打包，让 AI 能稳定复用——不是用什么工具，而是让 AI "知道怎么做对的事"。

---

> 🌐 **Language**: [English](./README_EN.md)

---

## ⚠️ 先说清楚：Skill 有多种含义

"Skill" 在 AI 领域不同语境下含义不同，避免混淆：

| 语境 | 含义 | 示例 |
|------|------|------|
| Claude Code 内置 Skill | CLI 内置的专门化子代理 | `/ask`、`/search`、`/loop` |
| 自定义斜杠命令 | 用户封装的快捷命令 | `commands.json` 中定义的 `/xxx` |
| Plugin Skill | 插件中封装的子代理 | 插件 `skills/` 目录下的 Skill |
| **Agent Skills（官方开放标准）** | **把领域知识打包成 SKILL.md 文件** | agentskills.io 发布的 Skill |

> **本仓库同时覆盖 Claude Code Skill 机制（立即能用）和 Agent Skills 开放标准（面向未来）**，让你既能用好 Claude Code 今天提供的 skill 能力，又能掌握跨平台的标准规范。

---

## 📚 系列仓库

本系列共三个仓库，帮你系统掌握 Claude Code 的核心概念：

| 仓库 | 主题 | 一句话描述 |
|------|------|-----------|
| 🔗 [what-is-agent](https://github.com/Wang-jiankai/what-is-agent) | **Agent** | AI 的"大脑"，能自主规划与执行任务 |
| 🔗 [what-is-skill](https://github.com/Wang-jiankai/what-is-skill) | **Skill** | AI 的"SOP 手册"，把专家经验结构化打包 |
| 🔗 [what-is-mcp](https://github.com/Wang-jiankai/what-is-mcp) | **MCP** | AI 的"接口标准"，连接外部世界的桥梁 |

---

## 📖 课程大纲（11 章）

### Part 1：Claude Code Skill 机制（立即能用）

| 章节 | 主题 | 一句话 |
|------|------|--------|
| 01 | [Skill 的多种含义](./concepts/01-skill的多重含义.md) | 厘清 Claude Code Skill 和 Agent Skills 的区别 |
| 02 | [内置 Skill 深度用法](./concepts/02-内置skill深度用法.md) | `/ask`、`/search`、`/loop`、`/simplify` 进阶技巧 |
| 03 | [自定义斜杠命令](./concepts/03-自定义斜杠命令.md) | 用 `commands.json` 封装高频操作 |
| 04 | [Plugin Skill 开发](./concepts/04-plugin-skill开发.md) | 在插件中创建 Skill 并调用工具 |
| 05 | [Skill 编排与组合](./concepts/05-skill编排与组合.md) | 多 Skill 协作完成复杂任务 |
| 06 | [团队 SOP 转斜杠命令](./concepts/06-团队SOP转斜杠命令.md) | 把团队标准流程变成一键命令 |

### Part 2：Agent Skills 开放标准（面向未来）

| 章节 | 主题 | 一句话 |
|------|------|--------|
| 07 | [SKILL.md 格式与结构](./concepts/07-SKILL.md格式与结构.md) | YAML 元数据 + Markdown 正文 |
| 08 | [渐进式披露原理](./concepts/08-渐进式披露原理.md) | Level 1/2/3 按需加载设计 |
| 09 | [写好 Instructions](./concepts/09-写好Instructions.md) | 把专家经验结构化、不模糊 |
| 10 | [Skill 编排与发布](./concepts/10-Skill编排与发布.md) | 多 Skill 协作 + agentskills.io 发布 |
| 11 | [发布你的第一个 Skill](./concepts/11-发布你的第一个Skill.md) | 从选题到发布的完整实战 |

---

## 🔰 什么是 Agent Skill？

**Agent Skill** 是一份结构化的"标准作业指导书"（SOP），以 `SKILL.md` 文件的形式打包领域知识，供 AI 在执行特定任务时加载使用。

### Skill 解决什么问题？

当前 AI Agent 的核心问题：**不稳定**。

- 这次能干活，下次步骤就丢
- 同一个任务，输出质量忽上忽下
- 换个说法，流程就跑偏

问题不在模型，而在**没有把"怎么做"的流程固化下来**。

### Skill 的核心原理

```
level 1（始终加载）：YAML 元数据（name + description）— AI 判断何时触发
level 2（按需加载）：SKILL.md 正文（Instructions）— 详细操作步骤
level 3（必要时加载）：scripts / references — 脚本和参考资料
```

这叫"**渐进式披露**"，不会塞爆 AI 的上下文窗口。

---

## 🚀 快速开始

### 方式一：学习 Claude Code Skill（今天就能用）

```bash
# 查看内置 Skill
/help

# 使用斜杠命令
/ask 这个模块怎么实现的？
/search 找出所有包含 token 的文件
/loop 每5分钟检查一次部署状态
```

### 方式二：创建自定义斜杠命令

```bash
mkdir -p ~/.claude
# 创建 commands.json，添加你的斜杠命令
```

### 方式三：学习 Agent Skills 标准

```bash
mkdir -p ~/.claude/skills/my-skill
# 创建 SKILL.md，开始编写你的第一个 Skill
```

---

## 📂 仓库目录结构

```
what-is-skill/
├── README.md              # 项目说明（中文）
├── README_EN.md          # 项目说明（英文）
├── LICENSE               # MIT 开源许可证
│
├── concepts/             # 📚 核心概念文章（11 章）
│   ├── 01-skill的多重含义.md
│   ├── 02-内置skill深度用法.md
│   ├── 03-自定义斜杠命令.md
│   ├── 04-plugin-skill开发.md
│   ├── 05-skill编排与组合.md
│   ├── 06-团队SOP转斜杠命令.md
│   ├── 07-SKILL.md格式与结构.md
│   ├── 08-渐进式披露原理.md
│   ├── 09-写好Instructions.md
│   ├── 10-Skill编排与发布.md
│   └── 11-发布你的第一个Skill.md
│
├── examples/             # 💡 Skill 示例
│   ├── 01-code-review-skill.md
│   ├── 02-meeting-notes-skill.md
│   ├── 03-api-design-skill.md
│   ├── 04-debug-skill.md
│   └── 05-data-analysis-skill.md
│
├── exercises/           # 🏋️ 练习题
│   └── ...
│
└── references/          # 📝 参考答案
    └── ...
```

---

## 📖 扩展学习

- [Agent Skills 官方标准](https://agentskills.io)
- [Anthropic Skills 官方仓库](https://github.com/anthropics/skills)
- [Claude Code Skills 文档](https://docs.anthropic.com/claude-code/skills)

---

## 🤝 贡献

欢迎提交你写的 Skill！如果你的仓库教的内容对你有帮助，欢迎提交 PR 分享你的学习成果或补充内容。

---

## 📄 许可证

MIT License © 2024-2026 Wang-jiankai
