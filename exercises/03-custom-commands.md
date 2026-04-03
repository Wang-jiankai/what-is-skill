# 03 | 练习：自定义斜杠命令

## 🎯 练习目标

- 掌握 `commands.json` 的规范格式
- 能把团队 SOP 封装成斜杠命令
- 理解项目级和用户级命令的区别

---

## 📋 练习要求

### 基础任务（必做）

**1. 找出以下 `commands.json` 的问题：**

```json
[
  {
    "name": "review code",
    "description": "代码审查",
    "prompt": "执行代码审查"
  }
]
```

问题在哪里？如何修正？

**2. 为以下 SOP 编写 `commands.json`：**

```json
[
  {
    "name": "test",
    "description": "运行测试套件",
    "prompt": "你是一个测试工程师..."
  }
]
```

补全 `prompt`，要求：
- 包含具体的测试执行步骤
- 包含输出格式（行覆盖率、函数覆盖率）
- 说明如何处理测试失败的情况

**3. 项目级 vs 用户级判断：**

| 命令 | 应该放哪里？ | 为什么？ |
|------|------------|---------|
| 团队统一的代码审查 SOP | | |
| 个人习惯的 changelog 生成 | | |
| 项目特有的构建命令 | | |
| Git 操作习惯封装 | | |

### 进阶任务（选做）

**把你团队最常用的 3 个操作封装成斜杠命令，写出完整的 `commands.json`。**

---

## 💡 提示

- 本练习对应的概念文章：[`concepts/03-custom-commands.md`](../concepts/03-custom-commands.md)
- 参考答案：[`references/03-custom-commands-solution.md`](../references/03-custom-commands-solution.md)
