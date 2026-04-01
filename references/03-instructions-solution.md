# 03 | 参考答案：写好 Instructions

## 📋 基础任务参考答案

### 任务 1：把专家经验转成 Instructions

> "发布 npm 包之前，要检查 package.json 的 version 字段是否正确，运行 tests 确保测试通过，然后用 npm publish 发布。记得检查 isPublishable 字段。"

**转成 Instructions：**

```markdown
## Steps

### Step 1：检查 package.json
- [ ] `version` 字段是否已更新（不能是 0.0.0）
- [ ] `isPublishable` 字段是否为 `true`（如有此字段）

### Step 2：运行测试
- [ ] 执行 `npm test`，确保所有测试通过
- [ ] 如有测试失败，不得发布

### Step 3：发布
- [ ] 执行 `npm publish`（注意：此操作不可逆）
- [ ] 记录发布的版本号
```

### 任务 2：Output Format 修正

❌ 原文（太模糊）：
```markdown
## Output Format
给出分析结果。
```

✅ 修正（规范）：
```markdown
## Output Format

发布报告必须包含：

```
## 📦 NPM 发布报告

### 版本
[version 字段值]

### 发布检查
- [ ] version 已更新
- [ ] 测试全部通过
- [ ] isPublishable 检查通过（如适用）

### 发布状态
[成功发布的版本号 / 失败原因]

### 注意事项
[如有]
```
```

### 任务 3：技术方案评审的触发条件和 Edge Cases

**触发条件应包含：**
```
触发关键词：tech design、方案评审、技术方案、设计评审、design review、ADR
触发场景：用户要求评审或讨论技术方案时
```

**不适用场景：**
```
不适用：用户只是想聊天、用户要求实现而非讨论方案、用户问具体代码问题而非架构问题
```
