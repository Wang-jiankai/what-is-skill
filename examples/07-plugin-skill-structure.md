# 07 | Plugin Skill 结构示例

本文档展示一个完整的 Plugin Skill 目录结构及其内容。

## 目录结构

```
my-plugin/
├── plugin.json
├── skills/
│   └── api-design/
│       ├── SKILL.md
│       ├── scripts/
│       │   ├── validate-openapi.sh
│       │   └── generate-client.sh
│       ├── references/
│       │   ├── rest-guidelines.md
│       │   └── error-codes.md
│       └── assets/
│           └── api-template.yaml
└── ...
```

## SKILL.md 示例

```yaml
---
name: api-design
description: API 设计评审 SOP。当用户说 "design API"、"API 规范"、"接口设计"、"review API" 时触发。
---

# API Design SOP

## When to Use
当用户要求设计新 API、审查现有 API、或询问 API 规范时触发。

## Prerequisites
- 用户提供了 API 需求描述，或
- 用户提供了现有 API 文档供审查

## API 设计原则

### RESTful 规范
1. 使用标准 HTTP 方法：GET/POST/PUT/DELETE
2. 资源命名使用名词：`/users`、`/orders`
3. 使用复数形式：`/users` 而非 `/user`
4. 嵌套资源限制在 2 层：`/users/{id}/orders`

### 路径设计
```
✅ 正确
GET /users/{id}
POST /users
GET /users/{id}/orders

❌ 错误
GET /getUser
POST /createUser
GET /users/{id}/orders/{orderId}/items/{itemId}
```

### 状态码规范
| 场景 | 状态码 |
|------|--------|
| 成功 | 200, 201, 204 |
| 客户端错误 | 400, 401, 403, 404 |
| 服务器错误 | 500, 502, 503 |

## 输出格式

### 对于新 API 设计
```
## API 设计提案

### 端点列表
| 方法 | 路径 | 描述 |
|------|------|------|
| GET | /users | 获取用户列表 |
| POST | /users | 创建用户 |

### 具体端点设计
#### GET /users

**Request**
```yaml
query:
  page: integer
  limit: integer
  sort: string
```

**Response**
```yaml
200:
  body:
    users: array
    pagination: object
```

### OpenAPI 验证结果
（运行 scripts/validate-openapi.sh 的结果）
```

### 对于 API 审查
```
## API 审查报告

### 规范符合度
- [x/❌] RESTful 路径规范
- [x/❌] HTTP 方法正确
- [x/❌] 状态码规范
- [x/❌] 错误响应格式

### 问题列表
1. [问题描述] - [位置] - [建议]

### 建议
（总体改进建议）
```

## 脚本使用

### validate-openapi.sh
验证 OpenAPI 规范的正确性：
```bash
scripts/validate-openapi.sh <api-file.yaml>
```

### generate-client.sh
根据 API 规范生成客户端代码：
```bash
scripts/generate-client.sh <api-file.yaml> <language>
```

## 参考资料

详细规范见：
- `references/rest-guidelines.md` — RESTful 设计指南
- `references/error-codes.md` — 错误码规范
```

## plugin.json 配置

```json
{
  "name": "api-design-plugin",
  "version": "1.0.0",
  "description": "API 设计辅助插件",
  "skills": [
    {
      "name": "api-design",
      "path": "./skills/api-design"
    }
  ]
}
```

## 与斜杠命令的区别

| 特性 | 自定义斜杠命令 | Plugin Skill |
|------|--------------|-------------|
| 定义位置 | `commands.json` | 插件 `skills/` 目录 |
| 工具调用 | ❌ | ✅ 可调用插件工具 |
| 分发 | 复制 JSON | 安装插件 |
| 复杂度 | 简单 | 较复杂 |

Plugin Skill 适合需要调用实际工具的复杂场景，简单的 prompt 指令用斜杠命令即可。
