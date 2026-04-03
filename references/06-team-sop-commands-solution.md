# 06 | 参考答案：团队 SOP 转斜杠命令

## 📋 基础任务参考答案

### 任务 1：完整的 commands.json

```json
[
  {
    "name": "setup-dev",
    "description": "新开发者环境搭建 SOP。当用户说 'setup'、'环境搭建'、'新机器'、'setup dev' 时触发。",
    "prompt": "你是一个 DevOps 专家。按照以下 SOP 帮助新开发者搭建开发环境。\n\n## 前置检查\n1. 确认操作系统（macOS/Linux/Windows）\n2. 确认已安装的依赖（Node.js >= 18、Docker >= 20）\n\n## 搭建步骤\n\n### Step 1：克隆代码仓库\n- 主仓库：`git clone git@github.com:company/main.git`\n- submodule（如有）：`git submodule update --init --recursive`\n\n### Step 2：安装依赖\n- npm install\n- 如果是 Docker 环境：`docker-compose up -d`\n\n### Step 3：环境配置\n- 复制 .env.example 到 .env\n- 填写必要的环境变量（如有疑问，先用 .env.example 中的注释做指引）\n\n### Step 4：启动服务\n- npm run dev\n\n### Step 5：验证\n- 访问 http://localhost:3000\n- 检查浏览器控制台是否有报错\n\n## 输出格式\n\n每完成一步报告：\n- ✅ Done / ❌ Failed + [原因]\n\n最终报告：\n```\n## 环境状态\n- [✅ Ready / ❌ Failed]\n- 失败的步骤：[步骤名] - [错误信息]\n- 访问地址：http://localhost:3000\n```"
  }
]
```

### 任务 2：分发方式选择

| 场景 | 应该用哪种分发方式？ |
|------|---------------------|
| 团队所有人统一使用 | 项目级（`.claude/commands.json`） |
| 个人习惯性操作 | 用户级（`~/.claude/commands.json`） |
| 不想暴露 SOP 内容给团队 | 用户级 |
| 快速迭代测试 | 用户级（先测试，成熟后迁移到项目级） |

---

## 继续学习

→ 下一章：[07 - SKILL.md 格式与结构](../concepts/07-skillmd-format.md)
