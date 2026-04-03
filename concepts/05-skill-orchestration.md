# 05 | Skill 编排与组合

## 🎯 学习目标

- 理解 Skill 编排的概念
- 掌握多 Skill 协作的常见模式
- 学会设计 Skill 之间的调用关系
- 避免 Skill 组合中的常见错误

---

## 什么是 Skill 编排？

Skill 编排（Orchestration）指的是：**如何让多个 Skill 协同工作，完成复杂任务**。

就像交响乐团需要一个指挥，每个乐器按乐谱在正确的时机演奏，Skill 编排也需要设计好：
- 哪个 Skill 先执行
- 下一个 Skill 什么时候触发
- 结果如何在 Skill 之间传递

---

## Skill 编排的常见模式

### 模式 1：顺序执行

一个 Skill 的输出作为下一个 Skill 的输入。

```
用户：review 并部署
    ↓
/ask 了解代码结构
    ↓
/review 执行代码审查
    ↓
/simplify 简化有问题的代码
```

### 模式 2：并行执行

多个独立的 Skill 同时执行，互不依赖。

```
用户：检查项目健康状态
    ↓
并行执行：
├── /search 检查测试覆盖率
├── /ask 检查文档完整性
└── /search 检查安全依赖
```

### 模式 3：条件分支

根据前一个 Skill 的结果，决定下一步执行哪个。

```
用户：修复这个 bug
    ↓
/ask 分析 bug 原因
    ↓
如果：需要数据库迁移 → /ask 显示迁移脚本
如果：只需修改代码 → /simplify 简化并修复
```

---

## Skill 编排实战

### 场景：完整的代码审查与修复流程

```
第一步：了解代码
    /ask 在 auth/ 目录下，认证逻辑是怎么实现的？

第二步：执行审查
    /review 审查 auth/ 目录的代码

第三步：根据审查结果行动
    如果有严重问题：
        → 标记问题，让用户确认
    如果有小问题：
        → 自动修复并展示 diff

第四步：验证修复
    /ask 验证修复是否正确
```

### 对应的 prompt 设计

```yaml
---
name: review-and-fix
description: 完整的代码审查与修复流程
---

# Review and Fix Workflow

## When to Use
当用户说 "review and fix" 或要求审查并修复代码时触发。

## Steps

1. **了解代码结构**
   使用 /ask 了解要审查的代码范围和结构

2. **执行代码审查**
   使用 /review 执行审查，收集 Critical Issues

3. **决策分支**
   - 如果 Critical Issues > 0：列出问题，等待用户确认
   - 如果 Critical Issues = 0：继续下一步

4. **自动修复**
   对每个小问题执行修复，展示 diff

5. **验证**
   使用 /ask 验证修复是否正确

## 输出格式
- 每一步的执行结果
- 最终状态总结
```

---

## Skill 组合的设计原则

### 1. 单一职责

每个 Skill 只做一件事：

```
❌ 一个 Skill 做所有事：
    "code-review-and-deploy" → 太复杂

✅ 多个 Skill 协作：
    /review → /fix → /test → /deploy
```

### 2. 清晰的输入输出

Skill 之间传递数据时，明确格式：

```yaml
## 输入格式
用户提供的代码文件路径

## 输出格式
{
  "critical_issues": [...],
  "suggestions": [...],
  "summary": "..."
}
```

### 3. 避免循环依赖

```
❌ 循环依赖：
    Skill A → Skill B → Skill A

✅ 有向无环：
    Skill A → Skill B → Skill C
```

---

## Claude Code 中的 Skill 协作

在 Claude Code 对话中，你可以通过**明确的指令**让多个 Skill 协作：

```
用 /review 审查 auth/ 目录，
如果有严重问题就停下来让我确认，
否则继续用 /simplify 简化代码，
最后用 /ask 验证修改是否正确。
```

Claude Code 会按顺序调用对应的 Skill。

---

## Skill 与 MCP 工具的组合

Skill 可以调用 MCP 工具，形成更强大的能力：

```
用户：检查这个 API 的文档是否完整

/ask 分析 API 端点列表
    ↓
MCP 工具查询文档系统
    ↓
比对并输出缺失的文档
```

### 示例配置

```yaml
---
name: api-doc-check
description: 检查 API 文档完整性
---

# API Doc Check Workflow

## When to Use
当用户说 "check API docs" 或要求检查 API 文档完整性时。

## Steps

1. 使用 /ask 获取当前代码库的 API 端点列表

2. 使用 `mcp__docs__search` 工具查询每个端点的文档

3. 比对并输出：
   - ✅ 已文档化
   - ⚠️ 文档缺失

4. 生成文档更新建议
```

---

## Skill 编排的注意事项

### 1. 注意上下文窗口

多个 Skill 的完整内容都会加载到上下文，如果 Skill 数量多或内容长，可能超出窗口。

**解决：** 每个 Skill 的 description 只保留触发信息，正文按需加载。

### 2. 权限累积

调用 MCP 工具时，权限是累积的。如果 `permissions.defaultMode: "auto"`，每个 Skill 的工具调用都需要单独授权。

### 3. disableSkillShellExecution

如果设置 `disableSkillShellExecution: true`，依赖 shell 的 Skill 会失败。在编排前确认设置。

---

## 📝 自我检测

- [ ] 能设计一个多 Skill 协作的流程吗？
- [ ] 知道如何避免 Skill 之间的循环依赖吗？

继续学习：[06 - 团队 SOP 转斜杠命令](./06-team-sop-commands.md)
