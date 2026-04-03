# 04 | Plugin Skill 开发

## 🎯 学习目标

- 理解 Plugin Skill 的定位和适用场景
- 学会在插件中创建 Skill
- 掌握 Plugin Skill 的文件结构
- 了解 Plugin Skill 与自定义斜杠命令的选择

---

## 什么是 Plugin Skill？

Plugin Skill 是**封装在插件中的 Skill**，通过插件的 `skills/` 目录定义，可以调用插件提供的工具。

**Plugin Skill vs 自定义斜杠命令：**

| 特性 | 自定义斜杠命令 | Plugin Skill |
|------|--------------|-------------|
| 定义方式 | `commands.json` | 插件 `skills/` 目录 |
| 工具调用 | ❌ 纯 prompt | ✅ 可调用插件提供的工具 |
| 复杂度 | 简单 | 较复杂 |
| 分发方式 | 复制 JSON 文件 | 安装插件包 |
| 适用场景 | 纯 prompt 指令 | 需要实际工具协作 |

---

## Plugin Skill 文件结构

```
my-plugin/
├── plugin.json           # 插件配置
├── skills/
│   └── my-skill/
│       ├── SKILL.md      # 必须：Skill 定义
│       ├── scripts/      # 可选：自动化脚本
│       ├── references/   # 可选：参考资料
│       └── assets/      # 可选：模板、图片等
└── ...
```

### SKILL.md 结构

```yaml
---
name: my-plugin-skill
description: 当用户说...或要求...时触发此 Skill
---

# My Plugin Skill

## When to Use
## Steps
## Output Format
```

---

## 实战：创建一个 Plugin Skill

### 步骤 1：创建 Skill 目录

```
my-plugin/
└── skills/
    └── code-review/
        ├── SKILL.md
        └── references/
            └── security-checklist.md
```

### 步骤 2：编写 SKILL.md

```yaml
---
name: code-review
description: 团队代码审查 SOP。当用户说 "review this PR"、"审查代码" 时触发。
---

# Code Review SOP

## When to Use
当用户要求审查代码或 review PR 时使用。

## Review Order（必须按顺序）

1. **安全性** — SQL 注入、XSS、硬编码密钥
2. **正确性** — 空值检查、边界条件、异常处理
3. **性能** — N+1 查询、循环优化
4. **风格** — 命名规范、注释完整性

## Output Format

必须包含：
- 🔴 Critical Issues
- 🟡 Suggestions
- ✅ Summary
```

### 步骤 3：添加 References（可选）

`skills/code-review/references/security-checklist.md`：

```markdown
# 安全审查清单

## SQL 注入检查
- [ ] 所有 SQL 查询是否使用参数化？
- [ ] 是否有字符串拼接的用户输入？

## XSS 检查
- [ ] 用户输入是否经过转义？
- [ ] 是否有 innerHTML 直接拼接？
```

### 步骤 4：在 plugin.json 中注册

```json
{
  "name": "my-plugin",
  "version": "1.0.0",
  "skills": [
    {
      "name": "code-review",
      "path": "./skills/code-review"
    }
  ]
}
```

---

## Plugin Skill 调用工具

Plugin Skill 的优势在于可以调用**插件提供的工具**。

### 示例：带工具调用的 Skill

```yaml
---
name: db-schema-review
description: 审查数据库 Schema 设计
---

# DB Schema Review SOP

## When to Use
当用户提供数据库 Schema 或要求审查数据库设计时触发。

## Steps

1. **加载 Schema 信息**
   - 如果用户提供文件路径，读取文件
   - 如果需要查询数据库，使用 `query_database` 工具

2. **执行审查**
   - 表命名规范
   - 字段类型选择
   - 索引设计
   - 外键关系

3. **输出报告**
```

在这个例子中，`query_database` 是插件提供的工具，Skill 指令告诉 Claude 什么时候、怎么使用它。

---

## 什么时候用 Plugin Skill？

### ✅ 适合用 Plugin Skill 的场景

- 需要调用插件提供的工具
- Skill 需要复用脚本或资源文件
- 需要版本管理和发布流程
- Skill 逻辑复杂，需要多文件组织

### ❌ 应该用自定义斜杠命令的场景

- 纯 prompt 指令，不需要工具
- 简单的一次性封装
- 不想开发完整插件

---

## Plugin Skill 的触发

Plugin Skill 通过两种方式触发：

1. **语义触发**：用户说的内容匹配 `description`
2. **显式调用**：`/plugin-name:skill-name`

### 示例

```
用户：帮我 review 这个 PR
→ 匹配 code-review Skill 的 description
→ Claude 加载 skills/code-review/SKILL.md
→ 按 SOP 执行审查
```

---

## Plugin Skill 开发注意事项

### 1. description 决定触发

```yaml
# ✅ 好的 description
description: 代码审查 SOP。当用户说 "review this PR" 或 "审查代码" 时触发。

# ❌ 模糊的 description
description: 做代码相关的事情。
```

### 2. 保持 Skill 独立

每个 Skill 应该是**自包含的**，不依赖其他 Skill 的状态。

### 3. 渐进式资源加载

- `name` + `description`：始终加载
- SKILL.md 正文：按需加载
- `references/`：必要时加载

### 4. 注意权限

Plugin Skill 调用工具时，同样受 `permissions.defaultMode` 控制。

---

## 📝 自我检测

- [ ] 能说出 Plugin Skill 和自定义斜杠命令的适用场景差异吗？
- [ ] 知道 Plugin Skill 的文件结构吗？

继续学习：[05 - Skill 编排与组合](./05-skill-orchestration.md)
