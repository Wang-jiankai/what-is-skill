# 02 | Claude Code 内置 Skill 深度用法

## 🎯 学习目标

- 掌握每个内置 Skill 的最佳使用场景
- 学会组合多个 Skill 完成复杂任务
- 避免常见的使用误区

---

## Claude Code 内置 Skill 概览

Claude Code 提供了以下内置 Skill：

| Skill | 命令 | 核心能力 |
|-------|------|---------|
| `/ask` | 问代码库相关问题 | 语义搜索 + 代码理解 |
| `/search` | 搜索代码库 | 正则 + 语义混合搜索 |
| `/loop` | 设置定时任务 | 循环监控与提醒 |
| `/simplify` | 简化代码 | 重构与清晰化 |
| `/claude-api` | API 使用指导 | Anthropic SDK 最佳实践 |
| `/update-config` | 修改配置文件 | JSON Schema 验证 |

---

## /ask — 语义问答

### 基础用法

```
/ask 这个模块的认证逻辑是怎么实现的？
```

### 深度技巧

**1. 限定范围**
```
/ask 在 auth/ 目录下，session 是怎么管理的？
```

**2. 对比分析**
```
/ask 比较 user-service 和 admin-service 的权限检查方式
```

**3. 追问深挖**
```
/ask 这个 token 过期后是怎么处理的？提示：找 refresh token 相关代码
```

### 最佳实践

- 问题越具体，答案越准确
- 可以一次问多个相关问题
- 善用"在...目录下"来限定搜索范围

---

## /search — 代码搜索

### 基础用法

```
/search 搜索所有包含 decrypt 的函数
```

### 深度技巧

**1. 正则搜索**
```
/search -r "async\s+function\s+\w+\s*\("
```

**2. 按文件类型筛选**
```
/search "password" --glob "*.ts"
```

**3. 找调用关系**
```
/search "getUserById" --callers
```

**4. 找被谁调用**
```
/search "getUserById" --callees
```

### 与 /ask 的区别

| 场景 | 用 /ask | 用 /search |
|------|---------|-----------|
| 理解"怎么实现的" | ✅ | ❌ |
| 找"哪些文件用了这个函数" | ❌ | ✅ |
| 搜索关键词 | ✅ | ✅ 更精确 |
| 正则匹配 | ❌ | ✅ |

---

## /loop — 定时循环任务

### 基础用法

```
/loop 每5分钟检查一下部署状态
```

### 深度技巧

**1. 条件触发**
```
/loop 每小时检查一次，如果有新的 error log 就通知我
```

**2. 多任务并行**
```
/loop 同时监控：
- GitHub Actions 状态
- 最新的 error log
- 磁盘使用率
```

**3. 设置终止条件**
```
/loop 每10分钟检查一次，当 CI 通过后停止
```

### 注意事项

- `disableSkillShellExecution: true` 时，依赖 shell 的 loop 会失败
- 建议设置明确的终止条件，避免无限循环
- 查看活跃 loop：`/loop --list`

---

## /simplify — 代码简化

### 基础用法

```
/simplify 帮我简化 auth/middleware.ts
```

### 深度技巧

**1. 只看改动**
```
/simplify 简化这个函数，但先展示 diff 再应用
```

**2. 指定风格**
```
/simplify 简化并保持 TypeScript 类型完整
```

**3. 解释后再改**
```
/simplify 解释为什么要这么改，然后执行
```

### 简化原则

- 单函数不超过 50 行
- 消除嵌套过深的条件
- 提取重复逻辑为 helper
- 保留关键注释和类型

---

## /claude-api — Anthropic API 指导

### 基础用法

```
/claude-api 怎么用流式输出？
```

### 深度技巧

**1. Agent 设计模式**
```
/claude-api 帮我设计一个客服 Agent，要考虑工具调用和上下文管理
```

**2. 上下文窗口优化**
```
/claude-api 在 200K token 上下文中，怎么设计高效的缓存策略？
```

**3. Tool Surface 设计**
```
/claude-api 设计一个 MCP Server 的工具列表，控制在 20 个以内
```

### 最新改进（v2.1.91）

`/claude-api` 在 v2.1.91 中增强了以下方面的指导：
- 工具设计决策
- 上下文管理策略
- 缓存最佳实践

---

## /update-config — 配置文件修改

### 基础用法

```
/update-config 添加一个新的 MCP Server
```

### 深度技巧

**1. 查看当前配置**
```
/update-config --show
```

**2. 验证配置**
```
/update-config --validate settings.json
```

**3. 批量修改**
```
/update-config set permissions.defaultMode to "auto"
```

### 常见配置项

| 配置项 | 说明 |
|--------|------|
| `mcpServers` | MCP Server 列表 |
| `permissions.defaultMode` | 权限模式 |
| `disableSkillShellExecution` | 禁用 Skill 中的 shell 执行 |
| `展級` | Claude Code 行为定制 |

---

## Skill 组合使用

多个 Skill 可以组合，完成复杂任务：

**示例：重构一个模块**
```
/ask 了解 auth 模块的当前结构
/search 找出所有相关的测试文件
/simplify 简化核心逻辑
/update-config 确保新的配置正确
```

---

## 📝 自我检测

- [ ] 能说出 /ask 和 /search 的使用场景差异吗？
- [ ] 知道 /loop 在 `disableSkillShellExecution: true` 下会怎样吗？

继续学习：[03 - 自定义斜杠命令](./03-自定义斜杠命令.md)
