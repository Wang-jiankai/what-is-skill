# ⚡ What is Skill?

> **"Skill" 是 AI 领域的 SOP 设计课。** 本仓库教你如何把人类专家的领域经验结构化打包，让 AI 能稳定复用——不是用什么工具，而是让 AI "知道怎么做对的事"。

---

> 🌐 **Language**: [English](./README_EN.md)

---

## ⚠️ 先说清楚：Skill 有多种含义

"Skill" 在 AI 领域不同语境下含义不同，避免混淆：

| 语境 | 含义 | 示例 |
|------|------|------|
| Claude Code `/skills` 命令 | Claude Code 的内置 Skill 功能 | `/skills` 查看已装 Skill |
| **Agent Skills（官方开放标准）** | **本仓库教学内容**：把领域知识打包成 SKILL.md 文件 | 官方发布在 agentskills.io |
| 民间泛称 | 有时把 MCP Tool 也叫 Skill | 容易混淆，不推荐 |

> **本仓库聚焦 Agent Skills 开放标准**，教你写高质量的 SKILL.md，让 AI 按你的 SOP 稳定工作。

---

## 📚 系列仓库

本系列共三个仓库，帮你系统掌握 Claude Code 的核心概念：

| 仓库 | 主题 | 一句话描述 |
|------|------|-----------|
| 🔗 [what-is-agent](https://github.com/Wang-jiankai/what-is-agent) | **Agent** | AI 的"大脑"，能自主规划与执行任务 |
| 🔗 [what-is-skill](https://github.com/Wang-jiankai/what-is-skill) | **Skill** | AI 的"SOP 手册"，把专家经验结构化打包 |
| 🔗 [what-is-mcp](https://github.com/Wang-jiankai/what-is-mcp) | **MCP** | AI 的"接口标准"，连接外部世界的桥梁 |

---

## 🔰 什么是 Agent Skill？

**Agent Skill** 是一份结构化的"标准作业指导书"（SOP），以 `SKILL.md` 文件的形式打包领域知识，供 AI 在执行特定任务时加载使用。

### Skill 解决什么问题？

当前 AI Agent 的核心问题：**不稳定**。

- 这次能干活，下次步骤就丢
- 同一个任务，输出质量忽上忽下
- 换个说法，流程就跑偏

问题不在模型，而在**没有把"怎么做"的流程固化下来**。

### Skill 和 MCP 的本质区别

| | MCP | Agent Skill |
|--|-----|------------|
| **解决什么问题** | AI 能访问什么外部工具 | AI 应该怎么做某类任务 |
| **本质** | 连接协议（AI 的"手"） | 知识打包（AI 的"技能书"） |
| **类比** | USB-C 接口 | 米其林厨师的操作手册 |
| **关系** | 可以组合用 | 可以组合用 |

### Skill 的核心原理

```
level 1（始终加载）：YAML 元数据（name + description）— AI 判断何时触发
level 2（按需加载）：SKILL.md 正文（Instructions）— 详细操作步骤
level 3（必要时加载）：scripts / references — 脚本和参考资料
```

这叫"**渐进式披露**"，不会塞爆 AI 的上下文窗口。

---

## 💡 核心概念

### 1. SKILL.md 结构
Skill 的核心文件。YAML 元数据 + Markdown 说明。

### 2. 渐进式披露
平时只加载 name/description，按需再加载完整内容。

### 3. 高质量 Instructions
把专家经验写成清晰的步骤，不依赖模型"即兴发挥"。

### 4. Skill 的编排与组合
多个 Skill 可以组合使用，按顺序或并行执行。

### 5. 从团队 SOP 到 Skill
把真实工作中的标准流程转成 Skill，实现 AI 自动化。

---

## 🛠️ Skill 示例

### 一个真实的高质量 Skill

```yaml
---
name: code-review
description: 团队代码审查 SOP——当用户说 "review this PR" 或 "审查代码" 时触发
---

# Code Review SOP

## 适用场景
用户让你审查代码或 review Pull Request。

## 审查顺序（必须按此顺序）

1. **安全性** — SQL 注入、XSS、敏感信息泄露、API 密钥硬编码
2. **逻辑正确性** — 边界条件、空指针、异常处理
3. **性能** — 循环优化、N+1 查询、数据库索引
4. **代码风格** — 命名规范、注释完整性

## 输出格式

必须包含以下三部分：

### 🔴 严重问题
（如果有）

### 🟡 建议改进
（如果有）

### ✅ 总评
- 优秀 / 通过 / 需要修改
```

### Skill 的文件结构

```
my-skill/
├── SKILL.md          # 必须：YAML 元数据 + Instructions
├── scripts/          # 可选：自动化脚本（可执行）
├── references/       # 可选：详细参考资料
└── assets/          # 可选：模板、图片
```

---

## 📂 仓库目录结构

```
what-is-skill/
├── README.md              # 项目说明（中文）
├── README_EN.md          # 项目说明（英文）
├── LICENSE               # MIT 开源许可证
│
├── concepts/             # 📚 核心概念文章
│   ├── 01-what-is-skill.md
│   ├── 02-skill-structure.md
│   ├── 03-writing-instructions.md
│   ├── 04-skill-composition.md
│   └── 05-real-world-practice.md
│
├── examples/             # 💡 真实 Skill 示例（SKILL.md 文件）
│   ├── 01-code-review-skill.md
│   ├── 02-meeting-notes-skill.md
│   ├── 03-api-design-skill.md
│   ├── 04-debug-skill.md
│   └── 05-data-analysis-skill.md
│
├── exercises/           # 🏋️ 练习题
│   ├── 01-basic-exercise.md
│   ├── 02-structure-exercise.md
│   ├── 03-instructions-exercise.md
│   ├── 04-composition-exercise.md
│   └── 05-practice-exercise.md
│
└── references/          # 📝 参考答案
    ├── 01-basic-solution.md
    ├── 02-structure-solution.md
    ├── 03-instructions-solution.md
    ├── 04-composition-solution.md
    └── 05-practice-solution.md
```

> **注意**：Skill 仓库的核心产物是 `.md` 文件（SKILL.md），不是 TypeScript 代码。所有 examples 都是真实的、可直接安装使用的 Skill。

---

## 🚀 运行说明

### 安装 Skill

Skill 以文件夹形式存在，安装方式有三种：

**方式一：放到项目目录（项目级）**
```bash
# 在项目根目录下创建
mkdir -p ./.claude/skills/my-skill
# 把 SKILL.md 放进去即可
```

**方式二：放到用户目录（全局）**
```bash
mkdir -p ~/.claude/skills/my-skill
```

**方式三：用 Claude Code 命令安装**
```
/plugin install xxx@anthropic-agent-skills
```

### 验证 Skill 是否生效

在 Claude Code 中问：
```
/skills
```
可以看到已安装的 Skill 列表。

或在对话中直接触发：
```
帮我 review 这个 PR
```
AI 会自动识别并加载对应的 Skill。

---

## 📖 扩展学习

- [Agent Skills 官方标准](https://agentskills.io)
- [Anthropic Skills 官方仓库](https://github.com/anthropics/skills)
- [Claude Code Skills 文档](https://docs.anthropic.com/claude-code/skills)

---

## 🤝 贡献

欢迎提交你写的 Skill！如果你有工作中的 SOP 想分享，提交 PR 即可。

---

## 📄 许可证

MIT License © 2024 Wang-jiankai
