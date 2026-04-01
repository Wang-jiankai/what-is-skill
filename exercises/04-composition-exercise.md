# 04 | 练习：Skill 的编排与组合

## 🎯 练习目标

- 理解 Skill 之间的并行与串行关系
- 掌握设计 Skill 触发优先级的方法
- 能识别并解决 Skill 冲突

---

## 📋 练习要求

### 基础任务（必做）

**1. 分析以下场景中的 Skill 关系：**

场景：用户说"帮我把这个新功能上线"

涉及的 Skill：
- `code-review`：审查代码
- `test-runner`：运行测试
- `deployment`：执行部署
- `monitoring-check`：检查监控

**问题：**
- 哪些 Skill 是并行的（可以同时存在）？
- 哪些 Skill 是串行的（前一个输出是后一个输入）？
- 请画出这个场景的 Skill 执行顺序图。

**2. 发现 Skill 冲突：**

```yaml
# Skill A
## Steps
1. 先写测试
2. 再写代码

# Skill B
## Steps
1. 直接写代码
2. 再补测试
```

这两个 Skill 冲突吗？为什么？
如何修正？

**3. 设计触发优先级：**

有两个 Skill 都可能匹配"设计数据库"的需求：
- `api-design`：通用 API 设计
- `database-schema`：数据库设计

如何通过命名和描述暗示触发优先级？

### 进阶任务（选做）

**为你常用的一个工作流，设计 3 个互相配合的 Skill，并说明它们的关系（并行/串行）。**

---

## 💡 提示

- 本练习对应的概念文章：[`concepts/04-skill-composition.md`](../concepts/04-skill-composition.md)
- 参考答案：[`references/04-composition-solution.md`](../references/04-composition-solution.md)
