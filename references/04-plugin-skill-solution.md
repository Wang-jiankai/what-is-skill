# 04 | 参考答案：Plugin Skill 开发

## 📋 基础任务参考答案

### 任务 1：选择题

| 场景 | 该用哪个？ | 理由 |
|------|----------|------|
| 需要调用插件提供的数据库查询工具 | **Plugin Skill** | 需要调用实际工具 |
| 纯 prompt 指令，不需要实际工具 | **自定义斜杠命令** | 简单场景不需要插件 |
| 想把 Skill 分发给其他 Claude Code 用户 | **Plugin Skill** | 插件更容易分发 |
| 团队 SOP 需要包含复杂的分支逻辑 | **Plugin Skill** | 可以组织复杂结构 |
| 想在 Skill 中调用 GitHub API | **Plugin Skill** | 需要 MCP 工具 |
| 临时封装一个简单的提醒功能 | **自定义斜杠命令** | 简单场景不需要插件 |

### 任务 2：Plugin Skill 目录结构设计

```
db-toolkit/
├── plugin.json
├── skills/
│   ├── schema-review/          # Skill 1
│   │   ├── SKILL.md
│   │   └── references/
│   │       └── schema-checklist.md
│   ├── sql-generator/          # Skill 2
│   │   ├── SKILL.md
│   │   └── scripts/
│   │       └── validate-sql.sh
│   └── data-dict/              # Skill 3
│       ├── SKILL.md
│       ├── assets/
│       │   └── dict-template.md
│       └── references/
│           └── field-types.md
└── ...
```

### 任务 3：判断对错

- [x] Plugin Skill 可以在 description 中引用 scripts/ 目录下的脚本 — **对**
- [x] Plugin Skill 的 SKILL.md 和 agentskills.io 的 SKILL.md 格式完全一样 — **对**：格式相同
- [x] 一个插件可以包含多个 Skill — **对**
- [x] Plugin Skill 触发后，Claude Code 会自动加载所有 Level 3 资源 — **错**：Level 3 只有在 Instructions 中明确引用时才加载

---

## 继续学习

→ 下一章：[05 - Skill 编排与组合](../concepts/05-skill编排与组合.md)
