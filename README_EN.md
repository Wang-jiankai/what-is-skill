# ⚡ What is Skill?

> **"Skill" is a SOP design methodology for the AI era — turning expert experience into reusable Standard Operating Procedures.** This repository explores the concepts and practice of Skill, teaching you how to structure domain expertise from human specialists into reusable, AI-executable knowledge packages — not which tools to use, but how to make AI consistently do things the *right* way.

---

> 🌐 **Language**: [中文](./README.md)

---

## ⚠️ Important: "Skill" Has Multiple Meanings

In the AI world, "Skill" means different things in different contexts:

| Context | Meaning | Example |
|---------|---------|---------|
| Claude Code `/skills` | Built-in Claude Code feature | `/skills` to list installed Skills |
| **Agent Skills (Official Open Standard)** | **This repository's focus**: domain knowledge packaged as SKILL.md | Official standard at agentskills.io |
| Community usage | Sometimes loosely refers to MCP Tools | Not recommended — causes confusion |

> **This repository focuses on the Agent Skills open standard** — teaching you to write high-quality SKILL.md files that make AI follow your SOP consistently.

---

## 📚 Series Repositories

This series contains three repositories to help you master the core concepts of Claude Code:

| Repository | Topic | One-liner |
|------------|-------|-----------|
| 🔗 [what-is-agent](https://github.com/Wang-jiankai/what-is-agent) | **Agent** | AI's "brain" — autonomously plans and executes tasks |
| 🔗 [what-is-skill](https://github.com/Wang-jiankai/what-is-skill) | **Skill** | AI's "SOP manual" — structured domain expertise packaging |
| 🔗 [what-is-mcp](https://github.com/Wang-jiankai/what-is-mcp) | **MCP** | AI's "interface standard" — bridge to the external world |

---

## 🔰 What is an Agent Skill?

An **Agent Skill** is a structured "Standard Operating Procedure" (SOP) packaged as a `SKILL.md` file, containing domain expertise that an AI can load and apply when executing specific tasks.

### What Problem Does Skill Solve?

Current AI Agents have a core reliability problem:

- Works this time, skips steps next time
- Same task, wildly different output quality
- Slight rephrasing breaks the entire workflow

The problem isn't the model — it's the **lack of structured procedural knowledge**.

### Skill vs MCP: The Key Distinction

| | MCP | Agent Skill |
|--|-----|-------------|
| **What it solves** | What external tools can AI access? | How should AI do this type of task? |
| **Nature** | Connection protocol (AI's "hand") | Knowledge packaging (AI's "recipe book") |
| **Analogy** | USB-C interface | Michelin chef's operating manual |
| **Relationship** | Can work together | Can work together |

### Core Principle: Progressive Disclosure

```
level 1 (always loaded): YAML metadata (name + description) — AI decides when to trigger
level 2 (on-demand): SKILL.md body (Instructions) — detailed procedure steps
level 3 (if needed): scripts / references — executable code and reference docs
```

---

## 💡 Core Concepts

### 1. What is Agent Skill
Understanding the problem Skill solves and how it differs from MCP.

### 2. SKILL.md Structure
YAML metadata + Markdown body. The anatomy of a real Skill file.

### 3. Writing High-Quality Instructions
The core skill: turning expert knowledge into clear, AI-executable steps.

### 4. Skill Composition & Chaining
Combining multiple Skills for complex workflows.

### 5. From Team SOP to Skill
Converting real-world workflows into installable Skills.

---

## 🛠️ Skill Examples

### A Real High-Quality Skill

```yaml
---
name: code-review
description: Team code review SOP — triggered when user says "review this PR" or "review code"
---

# Code Review SOP

## When to Use
Triggered when user asks for code review or PR review.

## Review Order (must follow this sequence)

1. **Security** — SQL injection, XSS, hardcoded secrets, API key exposure
2. **Correctness** — edge cases, null checks, exception handling
3. **Performance** — loop optimization, N+1 queries, missing indexes
4. **Style** — naming conventions, comment completeness

## Output Format

Must include these three sections:

### 🔴 Critical Issues
(if any)

### 🟡 Suggested Improvements
(if any)

### ✅ Overall Assessment
- Excellent / Approved / Needs Changes
```

### Skill File Structure

```
my-skill/
├── SKILL.md          # Required: YAML metadata + Instructions
├── scripts/          # Optional: executable scripts
├── references/       # Optional: detailed reference docs
└── assets/           # Optional: templates, images
```

---

## 📂 Repository Structure

```
what-is-skill/
├── README.md              # Project overview (Chinese)
├── README_EN.md          # Project overview (English)
├── LICENSE               # MIT License
│
├── concepts/             # 📚 Core concept articles
│   ├── 01-what-is-skill.md
│   ├── 02-skill-structure.md
│   ├── 03-writing-instructions.md
│   ├── 04-skill-composition.md
│   └── 05-real-world-practice.md
│
├── examples/             # 💡 Real Skill examples (SKILL.md files)
│   ├── 01-code-review-skill.md
│   ├── 02-meeting-notes-skill.md
│   ├── 03-api-design-skill.md
│   ├── 04-debug-skill.md
│   └── 05-data-analysis-skill.md
│
├── exercises/           # 🏋️ Exercises
│   ├── 01-basic-exercise.md
│   ├── 02-structure-exercise.md
│   ├── 03-instructions-exercise.md
│   ├── 04-composition-exercise.md
│   └── 05-practice-exercise.md
│
└── references/          # 📝 Reference solutions
    ├── 01-basic-solution.md
    ├── 02-structure-solution.md
    ├── 03-instructions-solution.md
    ├── 04-composition-solution.md
    └── 05-practice-solution.md
```

> **Note**: The Skill repository's core artifact is `.md` files (SKILL.md), not code. All examples are real, installable Skill files.

---

## 🚀 Getting Started

### Install a Skill

Skills are folder-based. Three ways to install:

**Method 1: Project-level**
```bash
mkdir -p ./.claude/skills/my-skill
# Place SKILL.md inside
```

**Method 2: User-level (global)**
```bash
mkdir -p ~/.claude/skills/my-skill
```

**Method 3: Via Claude Code command**
```
/plugin install xxx@anthropic-agent-skills
```

### Verify Installation

In Claude Code:
```
/skills
```
Shows all installed Skills.

Or trigger directly:
```
review this PR
```
AI will detect and load the matching Skill.

---

## 📖 Further Learning

- [Agent Skills Official Standard](https://agentskills.io)
- [Anthropic Skills Official Repo](https://github.com/anthropics/skills)
- [Claude Code Skills Documentation](https://docs.anthropic.com/claude-code/skills)

---

## 🤝 Contributing

Submit your own Skills! If you have a work SOP to share, just open a PR.

---

## 📄 License

MIT License © 2024 Wang-jiankai
