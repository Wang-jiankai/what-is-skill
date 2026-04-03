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

### Part 1: Claude Code Skill Mechanisms (Use Now)

| Chapter | Topic | Description |
|---------|-------|-------------|
| 01 | Skill Meanings | Claude Code `/skills`, Agent Skills, MCP Tools — sorting out the confusion |
| 02 | Built-in Skills Deep Dive | `/ask`, `/search`, `/loop`, `/simplify` advanced techniques |
| 03 | Custom Slash Commands | Package frequent operations with `commands.json` |
| 04 | Plugin Skill Development | Create Skills in plugins and call tools |
| 05 | Skill Orchestration | Multi-Skill collaboration for complex tasks |
| 06 | Team SOP to Slash Commands | Turn team standards into one-click commands |

### Part 2: Agent Skills Open Standard (Future-Ready)

| Chapter | Topic | Description |
|---------|-------|-------------|
| 07 | SKILL.md Format & Structure | YAML metadata + Markdown body |
| 08 | Progressive Disclosure | Level 1/2/3 on-demand loading design |
| 09 | Writing Instructions | Structure expert knowledge without ambiguity |
| 10 | Skill Orchestration & Publishing | Multi-Skill collaboration + agentskills.io publishing |
| 11 | Publish Your First Skill | Complete walkthrough from topic selection to publishing |

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
├── concepts/             # 📚 Core concept articles (11 chapters)
│   ├── 01-skill-meanings.md
│   ├── 02-builtin-skills-deep-dive.md
│   ├── 03-custom-commands.md
│   ├── 04-plugin-skills.md
│   ├── 05-skill-orchestration.md
│   ├── 06-team-sop-commands.md
│   ├── 07-skillmd-format.md
│   ├── 08-progressive-disclosure.md
│   ├── 09-writing-instructions.md
│   ├── 10-skill-orchestration-and-publishing.md
│   └── 11-publishing-first-skill.md
│
├── examples/             # 💡 Real Skill examples (SKILL.md files)
│   ├── 01-code-review-skill.md
│   ├── 02-meeting-notes-skill.md
│   ├── 03-api-design-skill.md
│   ├── 04-debug-skill.md
│   └── 05-data-analysis-skill.md
│
├── exercises/            # 🏋️ Exercises (one per chapter)
│   ├── 01-skill-meanings.md
│   ├── 02-builtin-skills-deep-dive.md
│   ├── 03-custom-commands.md
│   ├── 04-plugin-skills.md
│   ├── 05-skill-orchestration.md
│   ├── 06-team-sop-commands.md
│   ├── 07-skillmd-format.md
│   ├── 08-progressive-disclosure.md
│   ├── 09-writing-instructions.md
│   ├── 10-skill-orchestration-and-publishing.md
│   └── 11-publishing-first-skill.md
│
└── references/           # 📝 Reference solutions
    ├── 01-skill-meanings-solution.md
    ├── 02-builtin-skills-deep-dive-solution.md
    ├── 03-custom-commands-solution.md
    ├── 04-plugin-skills-solution.md
    ├── 05-skill-orchestration-solution.md
    ├── 06-team-sop-commands-solution.md
    ├── 07-skillmd-format-solution.md
    ├── 08-progressive-disclosure-solution.md
    ├── 09-writing-instructions-solution.md
    ├── 10-skill-orchestration-and-publishing-solution.md
    └── 11-publishing-first-skill-solution.md
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
