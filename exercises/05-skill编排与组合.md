# 05 | 练习：Skill 编排与组合

## 🎯 练习目标

- 理解并行和串行 Skill 的区别
- 能设计多 Skill 协作的流程
- 能识别并避免 Skill 冲突

---

## 📋 练习要求

### 基础任务（必做）

**1. 分析以下场景的 Skill 关系：**

场景：用户说"帮我把这个功能发布到生产环境"

涉及的 Skill：
- `code-review`：审查代码
- `test-runner`：运行测试
- `deploy-prod`：执行生产部署
- `smoke-test`：烟雾测试

问题：
- 这些 Skill 是并行还是串行关系？
- 画出执行顺序图（用箭头表示）
- 哪些可以并行，哪些必须串行？

**2. 发现并解决 Skill 冲突：**

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

- 这两个 Skill 冲突吗？
- 如果你是用户，在 Claude Code 中说"帮我写个功能"，AI 会选哪个？
- 如何在不删除任何一个 Skill 的情况下解决这个问题？

**3. 设计触发优先级：**

有两个 Skill：
- `api-design-rest`：RESTful API 设计规范
- `grpc-api-design`：gRPC API 设计规范

用户说："帮我设计一个用户服务的 API"

- 哪个 Skill 应该优先触发？
- 如何通过 description 暗示优先级？

### 进阶任务（选做）

**为你常用的工作流设计 3 个互相配合的 Skill：**

要求：
- 说明每个 Skill 的职责
- 画出它们的关系图（并行/串行）
- 描述它们如何协作完成一个完整任务

---

## 💡 提示

- 本练习对应的概念文章：[`concepts/05-skill编排与组合.md`](../concepts/05-skill编排与组合.md)
- 参考答案：[`references/05-skill-orchestration-solution.md`](../references/05-skill-orchestration-solution.md)
