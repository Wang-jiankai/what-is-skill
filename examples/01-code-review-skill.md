# 01 | 代码审查 Skill

```yaml
---
name: code-review
description: 团队代码审查 SOP。当用户说 "review this PR"、"审查代码"、"代码审查"、"review code" 时触发。
---

# Code Review SOP

## When to Use
当用户要求审查代码、review PR、或提交代码供审查时使用。

**触发关键词**：review、审查、PR review、代码检查、check code

**不适用**：
- 用户只是想聊天
- 用户要求修改代码（而非审查）
- 用户提供了具体修改指令

## Prerequisites
- 已获取需要审查的代码
- 如有 PR，确认 PR 链接或分支信息

## Review Order（必须按此顺序）

### 1. Security（安全性）— 必须首先完成
逐项检查：
- **SQL 注入**：是否有未参数化的 SQL 查询？
- **XSS**：是否有直接拼接用户输入到 HTML/JS？
- **硬编码密钥**：是否在代码中暴露了 API Key、密码、Token？
- **信息泄露**：错误信息是否泄露敏感信息？

### 2. Correctness（正确性）
- **空指针/空值**：是否对所有输入做了空值检查？
- **边界条件**：循环、数组访问是否考虑了边界？
- **异常处理**：是否捕获了可能的异常？

### 3. Performance（性能）
- **数据库查询**：是否有 N+1 查询问题？
- **循环优化**：是否有可优化的循环？
- **索引**：查询是否利用了索引？

### 4. Style（代码风格）
- **命名**：变量、函数命名是否清晰？
- **注释**：关键逻辑是否有注释？
- **格式**：是否通过 lint 检查？

## Critical Rule
- **Security 未通过，不得完成审查**
- 发现严重安全问题，必须在报告最前方标注

## Output Format

审查报告必须包含以下三部分，缺一不可：

```
## 🔴 Critical Issues
（如果没有，标注"未发现严重问题"）

## 🟡 Suggestions
（如果没有，标注"无建议改进项"）

## ✅ Summary
| 维度 | 结果 |
|------|------|
| Security | ✅ 通过 / ❌ 需修复 |
| Correctness | ✅ 通过 / ⚠️ 建议改进 |
| Performance | ✅ 通过 / ⚠️ 建议改进 |
| Style | ✅ 通过 / ⚠️ 建议改进 |

**总评**：[ ✅ 优秀  /  ✅ 通过  /  ❌ 需修改后重审 ]
```

## Examples

### Example 1：触发 Skill
```
用户：帮我 review 这个 PR
AI：[加载 code-review Skill] → 开始按 SOP 逐项审查
```

### Example 2：审查 Node.js 代码
```javascript
// 检查要点：
// Security: SQL 注入？XSS？硬编码密钥？
// Correctness: 参数验证？异常处理？
// Performance: 数据库查询效率？
```
