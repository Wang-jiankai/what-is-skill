# 06 | 团队 SOP 转斜杠命令

## 🎯 学习目标

- 理解如何把真实工作中的 SOP 变成 Claude Code 斜杠命令
- 学会分析 SOP 并提取关键步骤
- 掌握把专家经验结构化打包的技巧
- 能够为团队设计一套斜杠命令集

---

## 为什么团队需要斜杠命令？

团队中有很多**重复性高、标准化的操作**，比如：

- 代码审查
- 发布流程
- 环境搭建
- Bug 分类
- 需求评审

这些操作如果有 SOP，每次让 AI 手动按 SOP 执行，不仅慢，而且容易遗漏步骤。

**斜杠命令的价值：把 SOP 变成"一键执行"**。

---

## 把 SOP 转成斜杠命令的步骤

### Step 1：收集和整理现有 SOP

找到团队已有的 SOP 文档。比如：

```
/docs
├── onboarding/
│   └── new-dev-setup.md      # 新人环境搭建 SOP
├── code-review/
│   └── review-checklist.md   # 代码审查清单
├── release/
│   └── deployment.md         # 发布流程
└── bugs/
    └── triage.md            # Bug 分类 SOP
```

### Step 2：分析 SOP 结构

读取 SOP，提取：

- **触发条件**：什么时候用这个 SOP？
- **前置要求**：执行前需要什么？
- **步骤顺序**：必须按什么顺序执行？
- **输出格式**：最终产出是什么？
- **决策分支**：有哪些条件分支？

### Step 3：编写 commands.json

以新人环境搭建 SOP 为例：

```json
[
  {
    "name": "setup-dev",
    "description": "新开发者环境搭建 SOP",
    "prompt": "你是一个 DevOps 专家。按照以下 SOP 帮助新开发者搭建开发环境。\n\n## 前置检查\n1. 确认操作系统（macOS/Linux/Windows）\n2. 确认已安装的依赖（Node.js、Python、Docker 等）\n3. 确认代码仓库克隆状态\n\n## 搭建步骤（必须按顺序）\n\n### 1. 安装基础依赖\n- Node.js >= 18\n- Docker >= 20\n- Git\n\n### 2. 克隆代码仓库\n- 主仓库\n-  submodule（如有）\n\n### 3. 安装项目依赖\n```bash\nnpm install\n```\n\n### 4. 复制环境配置\n```bash\ncp .env.example .env\n```\n\n### 5. 启动本地服务\n```bash\ndocker-compose up -d\nnpm run dev\n```\n\n### 6. 验证\n- 访问 http://localhost:3000\n- 确认无报错日志\n\n## 输出格式\n每完成一步报告：✅ Done / ❌ Failed\n\n最终报告：\n- 环境状态：✅ Ready / ❌ Failed\n- 失败的步骤及错误信息"
  }
]
```

### Step 4：分发和使用

**项目级命令**（`.claude/commands.json`）：
- 适合团队统一的 SOP
- 所有人 clone 后即可使用

**用户级命令**（`~/.claude/commands.json`）：
- 适合个人习惯
- 不需要提交到代码仓库

---

## 实战：代码审查 SOP 转斜杠命令

### 原始 SOP

`docs/review-checklist.md`：

```markdown
# Code Review Checklist

## 1. Security
- SQL injection?
- XSS?
- Hardcoded secrets?
- Info disclosure?

## 2. Correctness
- Null checks?
- Edge cases?
- Exception handling?

## 3. Performance
- N+1 queries?
- Loop optimization?
- Index usage?

## 4. Style
- Naming conventions?
- Comments?
- Lint passed?

## Output Format
- Critical Issues
- Suggestions
- Summary
```

### 转成 commands.json

```json
[
  {
    "name": "review",
    "description": "团队代码审查 SOP",
    "prompt": "你是一个代码审查专家。按照以下 SOP 执行审查。\n\n## 审查顺序（必须严格按顺序）\n\n### 1. Security（安全性）— 必须首先完成\n- SQL 注入：是否有未参数化的 SQL？\n- XSS：是否有直接拼接用户输入？\n- 硬编码密钥：API Key、密码、Token 是否暴露？\n- 信息泄露：错误信息是否泄露敏感信息？\n\n### 2. Correctness（正确性）\n- 空值检查：所有输入是否验证？\n- 边界条件：循环、数组访问是否考虑边界？\n- 异常处理：是否捕获可能的异常？\n\n### 3. Performance（性能）\n- N+1 查询：是否有循环内查询？\n- 循环优化：是否有可优化的循环？\n- 索引：查询是否利用索引？\n\n### 4. Style（风格）\n- 命名：变量、函数命名是否清晰？\n- 注释：关键逻辑是否有注释？\n- 格式：是否通过 lint 检查？\n\n## 输出格式（严格按此格式）\n\n```\n## 🔴 Critical Issues\n（如果没有，标注\"未发现严重问题\"）\n\n## 🟡 Suggestions\n（如果没有，标注\"无建议改进项\"）\n\n## ✅ Summary\n| 维度 | 结果 |\n| Security | ✅ 通过 / ❌ 需修复 |\n| Correctness | ✅ 通过 / ⚠️ 建议改进 |\n| Performance | ✅ 通过 / ⚠️ 建议改进 |\n| Style | ✅ 通过 / ⚠️ 建议改进 |\n\n**总评**：[ ✅ 优秀 / ✅ 通过 / ❌ 需修改后重审 ]\n```\n\n## 使用方式\n\n```\n/review\n\n然后粘贴代码或 PR 链接\n```"
  }
]
```

---

## 团队斜杠命令集设计

建议团队设计一套统一的斜杠命令，覆盖常见场景：

```json
[
  {
    "name": "review",
    "description": "团队代码审查 SOP"
  },
  {
    "name": "test",
    "description": "运行测试套件并报告覆盖率"
  },
  {
    "name": "deploy-staging",
    "description": "部署到 staging 环境"
  },
  {
    "name": "deploy-prod",
    "description": "部署到生产环境"
  },
  {
    "name": "changelog",
    "description": "生成 CHANGELOG 条目"
  },
  {
    "name": "onboard",
    "description": "新开发者环境搭建 SOP"
  },
  {
    "name": "bug-triage",
    "description": "Bug 分类与优先级判定"
  }
]
```

### 命令命名规范

- 统一前缀（可选）：`team-*` 或 `dev-*`
- 动宾结构：`review`、`deploy-staging`、`bug-triage`
- 不超过 20 字符

---

## 斜杠命令的维护

### 版本管理

建议把 `commands.json` 纳入 Git 管理：

```
.claude/
└── commands.json      # 纳入版本控制
```

### 定期更新

当 SOP 变更时，同步更新 `commands.json`：
1. 修改 SOP 文档
2. 更新对应的 prompt
3. Pull Request 审查
4. 合并后所有人自动更新

### 文档同步

在 SOP 文档头部标注：

```markdown
---
关联斜杠命令：/review
最后更新：2026-04-03
---
```

---

## 📝 自我检测

- [ ] 能把团队 SOP 转成 commands.json 吗？
- [ ] 知道如何分发和维护斜杠命令吗？

继续学习：[07 - SKILL.md 格式与结构](./07-skillmd-format.md)
