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

### 内置 Skill 示例

```typescript
import { builtInSkills } from "@anthropic-ai/claude-code";

// 查看所有内置 Skill
console.log(builtInSkills.list());

// 内置 Skill 包括:
// - web_search: 网页搜索
// - file_read: 文件读取
// - file_write: 文件写入
// - code_execute: 代码执行
// - shell_command: Shell 命令执行
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
npx ts-node examples/basic.ts

# 运行技能链示例
npx ts-node examples/chaining.ts
```

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
