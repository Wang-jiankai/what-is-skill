# 03 | 参考答案：自定义斜杠命令

## 📋 基础任务参考答案

### 任务 1：`commands.json` 问题分析

```json
[
  {
    "name": "review code",    // ❌ 包含空格，应该用 kebab-case
    "description": "代码审查", // ❌ 太模糊，没有触发关键词
    "prompt": "执行代码审查"    // ❌ 太简单，没有结构化步骤
  }
]
```

**修正：**

```json
[
  {
    "name": "review",
    "description": "团队代码审查 SOP。当用户说 'review'、'审查代码'、'review code' 时触发。",
    "prompt": "你是一个代码审查专家。按照以下 SOP 执行审查：\n\n## 审查顺序\n1. Security（安全性）\n2. Correctness（正确性）\n3. Performance（性能）\n4. Style（风格）\n\n## 输出格式\n- 🔴 Critical Issues\n- 🟡 Suggestions\n- ✅ Summary"
  }
]
```

### 任务 2：补全 prompt

```json
{
  "name": "test",
  "description": "运行测试套件并报告覆盖率",
  "prompt": "你是一个测试工程师。执行以下操作：\n\n## 步骤\n\n### 1. 运行测试\n执行测试套件：`npm test`\n收集测试结果（通过/失败/跳过数量）\n\n### 2. 生成覆盖率报告\n执行覆盖率命令（如果有）：`npm run test:coverage`\n记录：行覆盖率、函数覆盖率、分支覆盖率\n\n### 3. 处理失败情况\n- 如果有测试失败：列出失败的测试名称和原因\n- 分析失败原因是代码问题还是测试本身问题\n- 建议修复方向\n\n## 输出格式\n\n```\n## 测试报告\n\n### 执行结果\n- 总测试数：X\n- 通过：X\n- 失败：X\n- 跳过：X\n\n### 覆盖率\n- 行覆盖率：XX%\n- 函数覆盖率：XX%\n- 分支覆盖率：XX%\n\n### 失败的测试（如有）\n1. [测试名称] - [失败原因]\n\n### 建议\n[根据覆盖率给出改进建议]\n```"
}
```

### 任务 3：项目级 vs 用户级

| 命令 | 应该放哪里？ | 为什么？ |
|------|------------|---------|
| 团队统一的代码审查 SOP | 项目级（`.claude/commands.json`） | 团队所有人统一使用，纳入版本控制 |
| 个人习惯的 changelog 生成 | 用户级（`~/.claude/commands.json`） | 个人习惯，不一定所有人需要 |
| 项目特有的构建命令 | 项目级 | 特定项目才需要 |
| Git 操作习惯封装 | 用户级 | 个人工作流习惯 |

---

## 继续学习

→ 下一章：[04 - Plugin Skill 开发](../concepts/04-plugin-skill开发.md)
