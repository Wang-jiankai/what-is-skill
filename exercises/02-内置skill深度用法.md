# 02 | 练习：内置 Skill 深度用法

## 🎯 练习目标

- 掌握 `/ask` 和 `/search` 的使用场景差异
- 理解 `/loop` 的限制条件
- 能组合使用多个内置 Skill

---

## 📋 练习要求

### 基础任务（必做）

**1. 选择正确的 Skill：**

| 场景 | 该用哪个？ |
|------|----------|
| "帮我理解 auth 模块的认证流程" | |
| "找出所有用了 password 字段的地方" | |
| "每隔5分钟检查一下 CI 状态" | |
| "简化这个复杂的嵌套函数" | |
| "这个 API 调用报错了，怎么修？" | |
| "我想用流式输出，怎么办？" | |

**2. `/ask` vs `/search` 区别实战：**

分别用 `/ask` 和 `/search` 回答以下问题，观察结果有什么不同：

问题："找出处理用户登录的代码"

- `/ask` 会返回什么？
- `/search` 会返回什么？
- 哪个更适合这个场景？

**3. `/loop` 限制分析：**

假设 `settings.json` 中设置了 `disableSkillShellExecution: true`，以下 `/loop` 命令会不会正常工作？

```
/loop 每分钟执行 echo "hello"
```

如果不能正常工作，应该怎么改？

### 进阶任务（选做）

**设计一个组合使用多个内置 Skill 的场景：**

场景：用户说"帮我把这个功能上线"

请设计使用哪些内置 Skill，按什么顺序，每个 Skill 负责什么。

---

## 💡 提示

- 本练习对应的概念文章：[`concepts/02-内置skill深度用法.md`](../concepts/02-内置skill深度用法.md)
- 参考答案：[`references/02-builtin-skill-solution.md`](../references/02-builtin-skill-solution.md)
