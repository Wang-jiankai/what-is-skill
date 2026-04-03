# 06 | 团队斜杠命令集示例

本文档展示一个完整的 `commands.json` 文件，包含团队常用的高频操作。

```json
[
  {
    "name": "review",
    "description": "团队代码审查 SOP",
    "prompt": "你是一个代码审查专家。按照以下 SOP 执行审查。\n\n## 审查顺序（必须按此顺序）\n\n### 1. Security（安全性）— 必须首先完成\n- SQL 注入：是否有未参数化的 SQL？\n- XSS：是否有直接拼接用户输入？\n- 硬编码密钥：API Key、密码、Token 是否暴露？\n- 信息泄露：错误信息是否泄露敏感信息？\n\n### 2. Correctness（正确性）\n- 空值检查：所有输入是否验证？\n- 边界条件：循环、数组访问是否考虑边界？\n- 异常处理：是否捕获可能的异常？\n\n### 3. Performance（性能）\n- N+1 查询：是否有循环内查询？\n- 循环优化：是否有可优化的循环？\n- 索引：查询是否利用索引？\n\n### 4. Style（风格）\n- 命名：变量、函数命名是否清晰？\n- 注释：关键逻辑是否有注释？\n- 格式：是否通过 lint 检查？\n\n## 输出格式（严格按此格式）\n\n```\n## 🔴 Critical Issues\n（如果没有，标注\"未发现严重问题\"）\n\n## 🟡 Suggestions\n（如果没有，标注\"无建议改进项\"）\n\n## ✅ Summary\n| 维度 | 结果 |\n| Security | ✅ 通过 / ❌ 需修复 |\n| Correctness | ✅ 通过 / ⚠️ 建议改进 |\n| Performance | ✅ 通过 / ⚠️ 建议改进 |\n| Style | ✅ 通过 / ⚠️ 建议改进 |\n\n**总评**：[ ✅ 优秀 / ✅ 通过 / ❌ 需修改后重审 ]\n```\n\n用户会提供代码或 PR 链接。"
  },
  {
    "name": "test",
    "description": "运行测试套件并报告覆盖率",
    "prompt": "你是一个测试工程师。执行以下操作：\n\n## 步骤\n\n### 1. 运行测试\n执行测试套件，收集结果。\n\n### 2. 生成报告\n输出格式如下：\n\n```\n## 测试报告\n\n### 执行结果\n- 总测试数：X\n- 通过：X\n- 失败：X\n- 跳过：X\n\n### 覆盖率\n- 行覆盖率：XX%\n- 函数覆盖率：XX%\n- 分支覆盖率：XX%\n\n### 失败的测试（如有）\n1. [测试名称] - [失败原因]\n\n### 建议\n（根据覆盖率给出改进建议）\n```"
  },
  {
    "name": "changelog",
    "description": "生成 CHANGELOG 条目",
    "prompt": "你是一个文档专家。根据以下 git log 信息，生成符合 Keep a Changelog 标准的 CHANGELOG 条目。\n\n## 要求\n- 使用 Conventional Commits 格式\n- 分成 Added / Changed / Fixed / Removed 四类\n- 每条改动一句话描述\n- 不包含 chore、docs 等非用户面向的改动\n\n## 输出格式\n\n```\n## [版本号] - YYYY-MM-DD\n\n### Added\n- 新功能描述\n\n### Changed\n- 功能变更描述\n\n### Fixed\n- Bug 修复描述\n\n### Removed\n- 移除的功能描述\n```\n\n用户会提供 git log 信息。"
  },
  {
    "name": "deploy-staging",
    "description": "部署到 staging 环境",
    "prompt": "你是一个 DevOps 专家。执行以下部署步骤：\n\n## 前置检查\n1. 确认在主分支或发布分支\n2. 确认 CI 所有检查通过\n3. 确认没有未提交的变更\n\n## 部署步骤\n1. 切换到 staging 分支\n2. 拉取最新代码\n3. 执行部署脚本：`./scripts/deploy-staging.sh`\n4. 等待服务启动\n5. 执行烟雾测试\n\n## 输出格式\n\n```\n## Staging 部署报告\n\n### 前置检查\n- [x/❌] 分支正确\n- [x/❌] CI 通过\n- [x/❌] 无未提交变更\n\n### 部署状态\n[成功/失败]\n\n### 烟雾测试\n- [x/❌] 服务启动正常\n- [x/❌] 健康检查通过\n\n### 访问地址\nhttp://staging.example.com\n```"
  },
  {
    "name": "bug-triage",
    "description": "Bug 分类与优先级判定",
    "prompt": "你是一个 Bug 分类专家。对用户提供的 Bug 报告进行分析和分类。\n\n## 分类标准\n\n### 按优先级\n- P0：核心功能不可用，影响所有用户，需要立即修复\n- P1：重要功能有问题，影响主要流程，24小时内修复\n- P2：功能有问题但有 workaround，影响部分用户，下个版本修复\n- P3：非关键问题，可接受，下个版本修复\n\n### 按类型\n- Security：安全相关\n- Performance：性能相关\n- UX：用户体验相关\n- Crash：崩溃相关\n- Other：其他\n\n## 输出格式\n\n```\n## Bug 分类报告\n\n### Bug 摘要\n[Bug 的一句话描述]\n\n### 优先级\n[P0/P1/P2/P3]\n\n### 类型\n[Security/Performance/UX/Crash/Other]\n\n### 原因分析\n（简要分析可能的原因）\n\n### 建议的修复步骤\n1. ...\n\n### 相关信息\n- 影响范围：\n- 复现步骤：\n```"
  }
]
```

## 使用方法

把这个 JSON 存为 `.claude/commands.json`（项目级）或 `~/.claude/commands.json`（用户级），然后在 Claude Code 中直接使用：

```
/review
/test
/changelog
/deploy-staging
/bug-triage
```
