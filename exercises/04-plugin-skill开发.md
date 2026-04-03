# 04 | 练习：Plugin Skill 开发

## 🎯 练习目标

- 理解 Plugin Skill 和自定义斜杠命令的适用场景
- 能设计一个 Plugin Skill 的目录结构
- 理解 SKILL.md 在插件中的写法

---

## 📋 练习要求

### 基础任务（必做）

**1. 选择题：什么时候用 Plugin Skill，什么时候用自定义斜杠命令？**

| 场景 | 该用哪个？ |
|------|----------|
| 需要调用插件提供的数据库查询工具 | |
| 纯 prompt 指令，不需要实际工具 | |
| 想把 Skill 分发给其他 Claude Code 用户 | |
| 团队 SOP 需要包含复杂的分支逻辑 | |
| 想在 Skill 中调用 GitHub API | |
| 临时封装一个简单的提醒功能 | |

**2. 设计一个 Plugin Skill 目录结构：**

场景：开发一个 `db-toolkit` 插件，包含以下功能：
- Schema 审查（需要调用数据库工具）
- SQL 生成（需要调用 LLM）
- 数据字典生成

请设计目录结构，包括：
- `skills/` 下的子目录
- 每个 Skill 需要的 optional 资源（scripts/references/assets）

**3. 判断对错：**

- [ ] Plugin Skill 可以在 description 中引用 scripts/ 目录下的脚本
- [ ] Plugin Skill 的 SKILL.md 和 agentskills.io 的 SKILL.md 格式完全一样
- [ ] 一个插件可以包含多个 Skill
- [ ] Plugin Skill 触发后，Claude Code 会自动加载所有 Level 3 资源

### 进阶任务（选做）

**为一个实际场景写一个 Plugin Skill 的 SKILL.md：**

场景：一个 `git-assistant` 插件，帮助团队进行 Git 操作

包含：
- commit-message 生成（根据 diff 生成符合 Conventional Commits 的 message）
- branch-cleanup（清理已合并的分支）
- tag 管理

---

## 💡 提示

- 本练习对应的概念文章：[`concepts/04-plugin-skill开发.md`](../concepts/04-plugin-skill开发.md)
- 参考答案：[`references/04-plugin-skill-solution.md`](../references/04-plugin-skill-solution.md)
