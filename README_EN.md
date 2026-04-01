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

### 5. Built-in Skills
Learn about system-provided base Skills for quick onboarding.

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
npx ts-node examples/01-basic.ts

# Run skill chaining example
npx ts-node examples/02-chaining.ts
```

---

## 📂 Repository Structure

```
what-is-skill/
├── README.md              # Project overview (Chinese)
├── README_EN.md          # Project overview (English)
├── LICENSE               # MIT License
├── package.json          # Project dependencies
├── tsconfig.json         # TypeScript configuration
├── .gitignore            # Git ignore rules
│
├── concepts/             # 📚 Core concept articles (read with assets/ for best experience)
│   ├── 01-what-is-skill.md
│   ├── 02-registration.md
│   ├── 03-invocation.md
│   ├── 04-chaining.md
│   └── 05-built-in-skills.md
│
├── examples/             # 💻 Runnable code examples (each maps to one concept)
│   ├── 01-basic.ts               # Maps to concepts/01: Skill definition basics
│   ├── 02-registration.ts       # Maps to concepts/02: Skill registration
│   ├── 03-invocation.ts         # Maps to concepts/03: Skill invocation
│   ├── 04-chaining.ts           # Maps to concepts/04: Skill chaining
│   └── 05-built-in.ts           # Maps to concepts/05: Built-in Skills
│
├── exercises/             # 🏋️ Exercises (one per concepts/ chapter)
│   ├── 01-basic-exercise.md
│   ├── 02-registration-exercise.md
│   ├── 03-invocation-exercise.md
│   ├── 04-chaining-exercise.md
│   └── 05-built-in-exercise.md
│
├── references/            # 📝 Exercise reference solutions (check after attempting)
│   ├── 01-basic-solution.ts
│   ├── 02-registration-solution.ts
│   ├── 03-invocation-solution.ts
│   ├── 04-chaining-solution.ts
│   └── 05-built-in-solution.ts
│
└── assets/                # 🖼️ Architecture & flow diagrams (referenced by concepts/)
    ├── skill-architecture.png       # Skill core architecture (read with concepts/01)
    ├── registration-flow.png        # Registration flow (read with concepts/02)
    ├── invocation-diagram.png       # Invocation diagram (read with concepts/03)
    ├── chaining-diagram.png         # Skill chaining diagram (read with concepts/04)
    └── built-in-overview.png        # Built-in Skills overview (read with concepts/05)
```

### Folder Responsibilities

| Folder | Content | Purpose |
|--------|---------|---------|
| `concepts/` | Theory articles, one per chapter | Build conceptual foundation |
| `examples/` | Runnable code, with concept mapping in header | Learn by doing |
| `exercises/` | Progressive exercises, one per chapter | Reinforce learning |
| `references/` | Reference solutions for exercises | Self-check after attempting |
| `assets/` | Diagrams referenced by `concepts/` articles | Visual aid |

### How to Use This Repository

Follow this path through the material:

```
Step 1  →  Read concepts/01 introductory article
           ↓
Step 2  →  Run examples/01 first code sample
           ↓
Step 3  →  Complete exercises/01 corresponding exercise
           ↓
Step 4  →  Check references/01 reference solution (self-review)
           ↓
Step 5  →  Move to next chapter (concepts/02 → examples/02 → ...)

Repeat until all 5 chapters are complete.
```

> **Tip:** Exercise difficulty increases with each chapter. Try to work through exercises independently before consulting `references/`.

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
