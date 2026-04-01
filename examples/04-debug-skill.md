# 04 | Bug 调试 Skill

```yaml
---
name: bug-debug
description: Bug 调试 SOP。当用户说 "debug"、"找 bug"、"修复错误"、"why is this broken" 时触发。
---

# Bug Debugging SOP

## When to Use
当用户要求调试代码、修复 Bug、或解释为什么代码出错时使用。

**触发关键词**：debug、找 bug、修复错误、why is this broken、doesn't work

**不适用**：
- 用户要求优化性能（用 performance-review Skill）
- 用户要求添加新功能

## Prerequisites
- 获取出错的代码或错误信息
- 获取错误日志（如有）

## Debug Steps

### Step 1：复现问题
- 在本地环境复现 Bug
- 记录复现步骤和错误信息

### Step 2：定位问题
按以下顺序排查：

**1. 查看错误信息**
- 错误类型（TypeError、ReferenceError、AssertionError...）
- 错误发生位置（文件名:行号）
- 调用栈（stack trace）

**2. 检查常见原因**
- **空值**：`undefined` 或 `null` 访问属性
- **类型错误**：期望的类型与实际不符
- **异步问题**：`await` 缺失或 Promise 未处理
- **作用域问题**：变量未定义或被覆盖

**3. 二分排查**
- 逐步注释代码，精确定位出错行
- 使用 `console.log` 或 debugger 确认执行路径

### Step 3：修复问题
- 修复后再次复现，确认问题解决
- 检查是否有副作用（是否引入新问题）

### Step 4：验证修复
- 编写或运行相关测试
- 确认边界情况正确处理

## Output Format

Bug 报告必须包含：

```
## 🐛 Bug 报告

### 问题描述
[Bug 的简要描述]

### 复现步骤
1. [步骤 1]
2. [步骤 2]
3. [步骤 3]

### 错误信息
```
[粘贴错误信息]
```

### 根因分析
[为什么出错？]

### 修复方案
```[代码修复]
```

### 验证结果
- [ ] 本地复现通过
- [ ] 相关测试通过
- [ ] 无副作用
```

## Examples

### Example 1：触发 Skill
```
用户：为什么我的登录接口报 500 错误？
AI：[加载 bug-debug Skill]
    → Step 1：复现（查看日志）→ Step 2：定位（发现是数据库连接池未关闭）
    → Step 3：修复 → Step 4：验证
```

### Example 2：用户贴错误信息
```
用户：TypeError: Cannot read property 'name' of undefined
AI：[加载 bug-debug Skill]
    → 根因：尝试访问 undefined 对象的 name 属性
    → 常见原因：后端返回的 data 为空 / 响应格式不对
    → 修复：加空值检查
```
