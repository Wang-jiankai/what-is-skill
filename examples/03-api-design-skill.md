# 03 | API 设计 Skill

```yaml
---
name: api-design
description: RESTful API 设计规范 SOP。当用户说 "design API"、"REST"、"接口设计"、"设计 API" 时触发。
---

# API Design SOP

## When to Use
当用户要求设计新的 API、评审 API 方案、或讨论 API 规范时使用。

**触发关键词**：API design、REST、接口设计、endpoint、API 规范

**不适用**：
- 用户只是想调用现有 API（用相应工具即可）
- 用户要求实现而非设计

## Prerequisites
- 确认需要设计的 API 所属系统/产品
- 确认主要使用者（前端、移动端、第三方）

## API Design Checklist

### 1. 资源命名（Resource Naming）
- 使用 **名词** 而非动词：`/users` 而非 `/getUsers`
- 使用 **复数**：`/orders` 而非 `/order`
- 使用 **小写 + 连字符**：`/user-profiles` 而非 `/userProfiles`
- 嵌套资源表关系：`/users/{userId}/orders`

### 2. HTTP 方法规范
| 操作 | 方法 | 示例 |
|------|------|------|
| 获取资源列表 | GET | `GET /users` |
| 获取单个资源 | GET | `GET /users/{id}` |
| 创建资源 | POST | `POST /users` |
| 更新资源（完整） | PUT | `PUT /users/{id}` |
| 更新资源（部分） | PATCH | `PATCH /users/{id}` |
| 删除资源 | DELETE | `DELETE /users/{id}` |

### 3. 状态码规范
| 情况 | 状态码 |
|------|--------|
| 成功 | 200 / 201 / 204 |
| 客户端错误 | 400（参数错误）/ 401（未认证）/ 403（无权限）/ 404（不存在）|
| 服务器错误 | 500 |

### 4. 错误响应格式
```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "参数验证失败",
    "details": [
      { "field": "email", "reason": "无效的邮箱格式" }
    ]
  }
}
```

### 5. 分页规范
- 使用 `limit` 和 `offset` 或 `cursor`
- 响应包含总数：`{ "data": [...], "total": 100, "limit": 20, "offset": 0 }`

### 6. 版本管理
- URL 路径：`/v1/users`
- Header：`API-Version: 2024-01-01`（可选）

## Output Format

API 设计文档必须包含：

```
## API 设计：[/资源名]

### Endpoint
[完整 URL，如 GET /v1/users/{userId}/orders]

### 方法
[GET / POST / PUT / PATCH / DELETE]

### 描述
[此 API 做什么]

### 请求
| 参数 | 类型 | 必须 | 说明 |
|------|------|------|------|

### 响应
| 状态码 | 说明 |
|--------|------|

### 示例
**Request：**
```bash
[示例命令]
```

**Response：**
```json
[示例响应]
```
```

## Critical Rules
- **所有写操作必须使用合适的 HTTP 方法**（POST/PUT/PATCH/DELETE）
- **所有变更必须幂等**（PUT 重复调用不会产生副作用）
- **敏感操作必须有鉴权**（401 或 403）
```
