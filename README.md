# ⚡ What is Skill?

> **"Skill" 让 AI 的能力边界无限扩展。** 本仓库面向零基础新手，通过清晰的概念讲解与可运行的代码示例，带你彻底理解什么是 Skill。

---

## 📚 系列仓库

本系列共三个仓库，帮你系统掌握 Claude Code 的核心概念：

| 仓库 | 主题 | 一句话描述 |
|------|------|-----------|
| 🔗 [what-is-agent](https://github.com/Wang-jiankai/what-is-agent) | **Agent** | AI 的"大脑"，能自主规划与执行任务 |
| 🔗 [what-is-skill](https://github.com/Wang-jiankai/what-is-skill) | **Skill** | AI 的"工具箱"，扩展能力的模块化插件 |
| 🔗 [what-is-mcp](https://github.com/Wang-jiankai/what-is-mcp) | **MCP** | AI 的"接口标准"，连接外部世界的桥梁 |

---

## 🔰 什么是 Skill？

**Skill（技能）** 是一种可复用、可组合的扩展单元，用于为 Agent 或 AI 系统添加新能力。

> **简单类比：** 如果把 Agent 看作一部智能手机，Skill 就是 App Store 里各种各样的应用。

### Skill 的核心特性

| 特性 | 说明 |
|------|------|
| **模块化** | 每个 Skill 都是独立的功能单元 |
| **可复用** | 一次编写，在多个 Agent 中使用 |
| **可组合** | 多个 Skill 可以协同工作 |
| **声明式** | 通过配置而非代码来启用/禁用 |

---

## 💡 核心概念

### 1. 技能定义（Skill Definition）
Skill 由名称、描述、参数 schema 和执行逻辑组成。

### 2. 技能注册（Skill Registration）
将 Skill 注册到 Agent 系统中，使其可被发现和调用。

### 3. 技能调用（Skill Invocation）
通过自然语言或 API 触发 Skill 执行。

### 4. 技能链（Skill Chaining）
将多个 Skill 按依赖顺序串联执行。

### 5. 内置技能（Built-in Skills）
了解系统自带的基础 Skill，快速上手。

---

## 🛠️ TypeScript 代码示例

### 定义一个基础 Skill

```typescript
import { Skill } from "@anthropic-ai/claude-code";

// 定义 Skill
const greetSkill = new Skill({
  name: "greet",
  description: "根据时间和用户名生成友好的问候语",
  parameters: {
    username: { type: "string", required: true },
    hour: { type: "number", required: false, default: new Date().getHours() }
  },
  async execute({ username, hour }) {
    const timeGreeting =
      hour < 12 ? "早上好" :
      hour < 18 ? "下午好" : "晚上好";

    return `${timeGreeting}，${username}！欢迎回来~`;
  }
});

// 使用 Skill
const result = await greetSkill.execute({ username: "小明" });
console.log(result); // 输出: 下午好，小明！欢迎回来~
```

### 技能链示例

```typescript
import { Agent, SkillRegistry } from "@anthropic-ai/claude-code";

// 注册多个 Skill
const registry = new SkillRegistry();
registry.register(greetSkill);
registry.register(weatherSkill);
registry.register(scheduleSkill);

// 创建一个使用技能链的 Agent
const agent = new Agent({
  model: "claude-opus-4-6",
  skillRegistry: registry,
  systemPrompt: "你是智能助手，会按顺序调用所需技能完成任务。"
});

// 自动调用技能链
const result = await agent.run(
  "先问候用户张三，然后告诉他今天北京的天气，最后查看他今天的日程"
);
console.log(result);
```

---

## 🚀 运行说明

### 前置要求

- Node.js ≥ 18
- npm 或 yarn
- TypeScript 编译器

### 安装

```bash
# 克隆仓库
git clone https://github.com/Wang-jiankai/what-is-skill.git
cd what-is-skill

# 安装依赖
npm install
```

### 运行示例

```bash
# 编译 TypeScript
npx tsc

# 运行基础示例
npx ts-node examples/01-basic.ts

# 运行技能链示例
npx ts-node examples/02-chaining.ts
```

---

## 📂 仓库目录结构

```
what-is-skill/
├── README.md              # 项目说明（中文）
├── README_EN.md          # 项目说明（英文）
├── LICENSE               # MIT 开源许可证
├── package.json          # 项目依赖配置
├── tsconfig.json         # TypeScript 编译配置
├── .gitignore            # Git 忽略文件
│
├── concepts/             # 📚 核心概念文章（与 assets/ 图片配合阅读效果更佳）
│   ├── 01-what-is-skill.md
│   ├── 02-registration.md
│   ├── 03-invocation.md
│   ├── 04-chaining.md
│   └── 05-built-in-skills.md
│
├── examples/             # 💻 可运行代码示例（每个文件对应一个核心概念）
│   ├── 01-basic.ts               # 对应 concepts/01：Skill 基础定义
│   ├── 02-registration.ts       # 对应 concepts/02：技能注册机制
│   ├── 03-invocation.ts         # 对应 concepts/03：技能调用方式
│   ├── 04-chaining.ts           # 对应 concepts/04：技能链编排
│   └── 05-built-in.ts           # 对应 concepts/05：内置技能使用
│
├── exercises/             # 🏋️ 练习题（每道题对应一篇 concepts/ 文章）
│   ├── 01-basic-exercise.md
│   ├── 02-registration-exercise.md
│   ├── 03-invocation-exercise.md
│   ├── 04-chaining-exercise.md
│   └── 05-built-in-exercise.md
│
├── references/            # 📝 练习参考答案（建议先独立完成再对照）
│   ├── 01-basic-solution.ts
│   ├── 02-registration-solution.ts
│   ├── 03-invocation-solution.ts
│   ├── 04-chaining-solution.ts
│   └── 05-built-in-solution.ts
│
└── assets/                # 🖼️ 架构图、流程图（供 concepts/ 文章引用）
    ├── skill-architecture.png       # Skill 核心架构图（配合 concepts/01 阅读）
    ├── registration-flow.png        # 注册流程图（配合 concepts/02 阅读）
    ├── invocation-diagram.png       # 调用流程图（配合 concepts/03 阅读）
    ├── chaining-diagram.png         # 技能链编排图（配合 concepts/04 阅读）
    └── built-in-overview.png        # 内置技能总览图（配合 concepts/05 阅读）
```

### 文件夹职责

| 文件夹 | 内容 | 用途 |
|--------|------|------|
| `concepts/` | 核心理论文章，每篇讲一个知识点 | 帮助新手建立概念框架 |
| `examples/` | 精心设计的可运行代码，顶部标注对应概念 | 边学边实践 |
| `exercises/` | 难度递进的练习（与 concepts/ 章节一一对应）| 巩固学习效果 |
| `references/` | 对应练习的参考解答 | 供对照自查 |
| `assets/` | 架构图、流程图，供 `concepts/` 文章引用 | 辅助理解 |

### 如何使用本仓库

推荐按以下路径依次学习：

```
第 1 步  →  阅读 concepts/01 入门文章
           ↓
第 2 步  →  运行 examples/01 第一个代码示例
           ↓
第 3 步  →  完成 exercises/01 对应练习
           ↓
第 4 步  →  查阅 references/01 参考答案（自查）
           ↓
第 5 步  →  进入下一章（concepts/02 → examples/02 → ...）

循环往复，直至完成全部 5 章。
```

> **提示：** `exercises/` 的习题难度随章节递增。建议先独立思考，实在卡住再看 `references/`。

---

## 📖 扩展学习

- [Claude Skill 官方文档](https://docs.anthropic.com/claude-code/skills)
- [Skill 开发指南](https://github.com/anthropics/claude-code/tree/main/skills)
- [Awesome Claude Skills](https://github.com/topics/claude-skill)

---

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

---

## 📄 许可证

MIT License © 2024 Wang-jiankai
