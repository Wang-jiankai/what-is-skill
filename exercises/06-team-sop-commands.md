# 06 | 练习：团队 SOP 转斜杠命令

## 🎯 练习目标

- 能分析团队 SOP 的结构
- 能把 SOP 转成 `commands.json` 中的 prompt
- 理解斜杠命令的维护和分发机制

---

## 📋 练习要求

### 基础任务（必做）

**把以下团队 SOP 转成斜杠命令：**

**SOP 来源**：新人开发环境搭建 SOP

```
新人开发环境搭建流程：

1. 前置检查
   - 确认操作系统（macOS/Linux/Windows）
   - 确认已安装的依赖（Node.js >= 18、Docker >= 20）

2. 克隆代码仓库
   - 主仓库：`git clone git@github.com:company/main.git`
   - submodule（如有）：`git submodule update --init --recursive`

3. 安装依赖
   - npm install
   - 如果是 Docker 环境：docker-compose up -d

4. 环境配置
   - 复制 .env.example 到 .env
   - 填写必要的环境变量

5. 启动服务
   - npm run dev

6. 验证
   - 访问 http://localhost:3000
   - 确认无报错
```

**要求：**
- 写出完整的 `commands.json` 片段
- 包含规范的 prompt
- 包含输出格式（每一步报告状态）

**2. 分发方式选择：**

| 场景 | 应该用哪种分发方式？ |
|------|---------------------|
| 团队所有人统一使用 | |
| 个人习惯性操作 | |
| 不想暴露 SOP 内容给团队 | |
| 快速迭代测试 | |

### 进阶任务（选做）

**调研你团队的 3 个核心 SOP，把其中一个写成完整的 `commands.json` 并说明：**

- 为什么选这个 SOP？
- 分发方式是什么（项目级/用户级）？
- 如何保持 SOP 和斜杠命令的同步？

---

## 💡 提示

- 本练习对应的概念文章：[`concepts/06-team-sop-commands.md`](../concepts/06-team-sop-commands.md)
- 参考答案：[`references/06-team-sop-commands-solution.md`](../references/06-team-sop-commands-solution.md)
