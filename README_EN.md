# ⚡ What is Skill?

> **"Skill" expands the boundaries of AI capabilities.** This repository is designed for absolute beginners, helping you thoroughly understand what a Skill is through clear concept explanations and runnable code examples.

---

## 📚 Series Repositories

This series contains three repositories to help you master the core concepts of Claude Code:

| Repository | Topic | One-liner |
|------------|-------|-----------|
| 🔗 [what-is-agent](https://github.com/Wang-jiankai/what-is-agent) | **Agent** | AI's "brain" — autonomously plans and executes tasks |
| 🔗 [what-is-skill](https://github.com/Wang-jiankai/what-is-skill) | **Skill** | AI's "toolbox" — modular plugins that extend capabilities |
| 🔗 [what-is-mcp](https://github.com/Wang-jiankai/what-is-mcp) | **MCP** | AI's "interface standard" — a bridge to the external world |

---

## 🔰 What is a Skill?

A **Skill** is a reusable, composable unit of extension that adds new capabilities to an Agent or AI system.

> **Simple analogy:** If an Agent is a smartphone, Skills are the various apps in the App Store.

### Core Skill Characteristics

| Characteristic | Description |
|----------------|-------------|
| **Modular** | Each Skill is an independent functional unit |
| **Reusable** | Write once, use across multiple Agents |
| **Composable** | Multiple Skills can work together |
| **Declarative** | Enable/disable via configuration, not code |

---

## 💡 Core Concepts

### 1. Skill Definition
A Skill consists of a name, description, parameter schema, and execution logic.

### 2. Skill Registration
Register a Skill with the Agent system so it can be discovered and invoked.

### 3. Skill Invocation
Trigger Skill execution via natural language or API.

### 4. Skill Chaining
Chain multiple Skills together and execute them in dependency order.

---

## 🛠️ TypeScript Code Examples

### Define a Basic Skill

```typescript
import { Skill } from "@anthropic-ai/claude-code";

// Define a Skill
const greetSkill = new Skill({
  name: "greet",
  description: "Generates a friendly greeting based on time and username",
  parameters: {
    username: { type: "string", required: true },
    hour: { type: "number", required: false, default: new Date().getHours() }
  },
  async execute({ username, hour }) {
    const timeGreeting =
      hour < 12 ? "Good morning" :
      hour < 18 ? "Good afternoon" : "Good evening";

    return `${timeGreeting}, ${username}! Welcome back~`;
  }
});

// Use the Skill
const result = await greetSkill.execute({ username: "Alice" });
console.log(result); // Output: Good afternoon, Alice! Welcome back~
```

### Skill Chaining

```typescript
import { Agent, SkillRegistry } from "@anthropic-ai/claude-code";

// Register multiple Skills
const registry = new SkillRegistry();
registry.register(greetSkill);
registry.register(weatherSkill);
registry.register(scheduleSkill);

// Create an Agent using skill chaining
const agent = new Agent({
  model: "claude-opus-4-6",
  skillRegistry: registry,
  systemPrompt: "You are an intelligent assistant. Call Skills in sequence to complete tasks."
});

// Automatically invoke skill chain
const result = await agent.run(
  "First greet user Zhang San, then tell him the weather in Beijing today, and finally check his schedule for today"
);
console.log(result);
```

### Built-in Skill Examples

```typescript
import { builtInSkills } from "@anthropic-ai/claude-code";

// List all built-in Skills
console.log(builtInSkills.list());

// Built-in Skills include:
// - web_search: Web search
// - file_read: File reading
// - file_write: File writing
// - code_execute: Code execution
// - shell_command: Shell command execution
```

---

## 🚀 Getting Started

### Prerequisites

- Node.js ≥ 18
- npm or yarn
- TypeScript compiler

### Installation

```bash
# Clone the repository
git clone https://github.com/Wang-jiankai/what-is-skill.git
cd what-is-skill

# Install dependencies
npm install
```

### Run Examples

```bash
# Compile TypeScript
npx tsc

# Run basic example
npx ts-node examples/basic.ts

# Run skill chaining example
npx ts-node examples/chaining.ts
```

---

## 📖 Further Learning

- [Claude Skill Official Docs](https://docs.anthropic.com/claude-code/skills)
- [Skill Development Guide](https://github.com/anthropics/claude-code/tree/main/skills)
- [Awesome Claude Skills](https://github.com/topics/claude-skill)

---

## 🤝 Contributing

Issues and Pull Requests are welcome!

---

## 📄 License

MIT License © 2024 Wang-jiankai
