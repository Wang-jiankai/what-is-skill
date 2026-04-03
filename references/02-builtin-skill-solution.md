# 02 | 参考答案：内置 Skill 深度用法

## 📋 基础任务参考答案

### 任务 1：选择正确的 Skill

| 场景 | 该用哪个？ | 理由 |
|------|----------|------|
| "帮我理解 auth 模块的认证流程" | `/ask` | 需要理解代码逻辑和结构 |
| "找出所有用了 password 字段的地方" | `/search` | 需要精确搜索代码 |
| "每隔5分钟检查一下 CI 状态" | `/loop` | 定时循环任务 |
| "简化这个复杂的嵌套函数" | `/simplify` | 代码简化重构 |
| "这个 API 调用报错了，怎么修？" | `/ask` | 理解问题并给出解决方案 |
| "我想用流式输出，怎么办？" | `/claude-api` | API 使用指导 |

### 任务 2：`/ask` vs `/search` 区别

**`/ask` 适合**：理解"怎么实现的"、解释代码逻辑、分析架构
**`/search` 适合**：找"哪些文件用了这个"、精确搜索关键词、按模式匹配

对于"找出处理用户登录的代码"：
- `/search` 更精确，可以找出所有相关文件和代码位置
- `/ask` 会给出一个解释性的回答，可能不完整

### 任务 3：`/loop` 限制分析

如果 `disableSkillShellExecution: true`，`/loop` 会失败，因为 `/loop` 依赖 shell 执行定时任务。

**替代方案**：
- 使用外部调度器（cron、GitHub Actions）触发 Claude Code
- 在 `settings.json` 中设置 `disableSkillShellExecution: false`
- 使用 MCP 工具实现定时检查

---

## 继续学习

→ 下一章：[03 - 自定义斜杠命令](../concepts/03-自定义斜杠命令.md)
