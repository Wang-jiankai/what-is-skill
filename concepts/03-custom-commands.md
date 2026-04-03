# 03 | 自定义斜杠命令

## 🎯 学习目标

- 理解 `commands.json` 的结构和字段
- 学会把自己的常用操作封装成斜杠命令
- 掌握斜杠命令的最佳实践

---

## 什么是自定义斜杠命令？

自定义斜杠命令让你把**高频操作封装成 `/xxx` 快捷命令**，在 Claude Code 中随时调用。

它通过 `commands.json` 配置文件定义，存放在：
- **项目级**：`项目根目录/.claude/commands.json`
- **用户级**：`~/.claude/commands.json`

---

## commands.json 结构

```json
[
  {
    "name": "cmd-name",
    "description": "命令的简短描述",
    "prompt": "详细的指令..."
  }
]
```

### 字段说明

| 字段 | 必须 | 说明 |
|------|------|------|
| `name` | ✅ | 命令名（英文、kebab-case） |
| `description` | ✅ | 一句话描述，显示在 /help 中 |
| `prompt` | ✅ | 触发时给 AI 的指令 |

---

## 实战示例

### 示例 1：代码审查命令

```json
[
  {
    "name": "review",
    "description": "执行团队代码审查 SOP",
    "prompt": "你是一个代码审查专家。按照以下 SOP 执行审查：\n\n## 审查顺序\n1. 安全性：SQL注入、XSS、硬编码密钥\n2. 正确性：空值检查、边界条件、异常处理\n3. 性能：N+1查询、循环优化\n4. 风格：命名规范、注释完整性\n\n## 输出格式\n必须包含：\n- 🔴 Critical Issues\n- 🟡 Suggestions\n- ✅ Summary\n\n请审查用户提供的代码或 PR。"
  }
]
```

### 示例 2：生成 Changelog

```json
[
  {
    "name": "changelog",
    "description": "根据 git commit 生成 CHANGELOG",
    "prompt": "你是一个文档专家。根据以下 git log 信息，生成符合 Keep a Changelog 标准的 CHANGELOG 条目。\n\n要求：\n- 使用 Conventional Commits 格式\n- 分成 Added / Changed / Fixed / Removed 四类\n- 每条改动一句话描述\n- 不包含 chore、docs 等非用户面向的改动\n\n用户会提供 git log 信息。"
  }
]
```

### 示例 3：生成 README 摘要

```json
[
  {
    "name": "readme-check",
    "description": "检查 README 是否完整",
    "prompt": "你是一个技术文档审查员。检查当前项目的 README.md 是否包含以下内容：\n\n必须包含：\n- 项目简介（一句话）\n- 安装方法\n- 快速开始\n- 主要功能列表\n- 贡献指南\n\n如果缺少任何一项，指出具体缺少什么，并给出补充建议。"
  }
]
```

---

## 项目级 vs 用户级

| 作用域 | 位置 | 生效范围 |
|--------|------|---------|
| 项目级 | `.claude/commands.json` | 仅当前项目 |
| 用户级 | `~/.claude/commands.json` | 所有项目 |

**最佳实践：**
- 项目级：放团队统一的 SOP 命令（如 `review`、`test`）
- 用户级：放个人习惯命令（如 `changelog`、`readme-check`）

---

## 命令命名规范

- **格式**：kebab-case（字母、数字、连字符）
- **长度**：不超过 20 字符
- **唯一性**：同一作用域内不可重名
- **语义化**：`review` 比 `cmd1` 好

### ✅ 好的命名
```
/review
/changelog
/deploy-staging
/api-test
```

### ❌ 不好的命名
```
/cmd1
/r
/review-the-code-for-bugs-please
```

---

## prompt 编写技巧

### 1. 结构化指令

```
❌ 模糊：
"帮我审查代码"

✅ 结构化：
"你是一个代码审查专家。审查时必须按以下顺序：
1. 安全性检查
2. 逻辑正确性检查
3. 性能检查
输出格式必须包含：Critical Issues / Suggestions / Summary"
```

### 2. 包含触发条件

```json
{
  "prompt": "当用户说 '/deploy' 或要求部署时，执行以下操作：\n\n## 前置检查\n1. 确认在主分支\n2. 确认 CI 通过\n3. 确认没有未提交的变更\n\n## 部署步骤\n..."
}
```

### 3. 明确输出格式

```json
{
  "prompt": "执行代码审查，输出格式如下（严格按此格式）：\n\n## 🔴 Critical Issues\n...\n\n## 🟡 Suggestions\n...\n\n## ✅ Summary\n| 维度 | 结果 |\n..."
}
```

---

## 调试斜杠命令

### 查看所有命令

```
/help
```

### 测试命令

```
/review
```

如果没有生效，检查：
1. `commands.json` 格式是否 valid JSON
2. 文件是否在正确位置
3. 命令名是否拼写正确

---

## 与 Plugin Skill 的区别

| 特性 | 自定义斜杠命令 | Plugin Skill |
|------|--------------|-------------|
| 定义方式 | `commands.json` | 插件代码 |
| 可调用外部工具 | ❌（仅 prompt） | ✅（可调用插件提供的工具） |
| 需要开发插件 | ❌ | ✅ |
| 分发方式 | 复制 `commands.json` | 安装插件包 |
| 适用场景 | 纯 prompt 指令 | 需要调用实际工具 |

---

## 📝 自我检测

- [ ] 能写出一个规范的 `commands.json` 吗？
- [ ] 知道项目级和用户级命令的优先级吗？

继续学习：[04 - Plugin Skill 开发](./04-plugin-skills.md)
