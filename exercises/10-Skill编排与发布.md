# 10 | 练习：Skill 编排与发布

## 🎯 练习目标

- 理解 Skill 之间的并行与串行关系
- 掌握设计 Skill 触发优先级的方法
- 能识别并解决 Skill 冲突
- 了解发布到 agentskills.io 的流程

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

**3. 发布流程排序：**

把以下步骤按正确顺序排列：

```
A. 在 Claude Code 中测试
B. 编写完整的 SKILL.md
C. 提交到 agentskills.io
D. 确定 Skill 的使用场景
E. 收集用户反馈并迭代
```

正确的顺序应该是：___ → ___ → ___ → ___ → ___

### 进阶任务（选做）

**为你常用的一个工作流，设计 3 个互相配合的 Skill，并说明它们的关系（并行/串行），然后模拟发布流程。**

---

## 💡 提示

- 本练习对应的概念文章：[`concepts/10-Skill编排与发布.md`](../concepts/10-Skill编排与发布.md)
- 参考答案：[`references/10-skill-orchestration-refactor.md`](../references/10-skill-orchestration-refactor.md)
