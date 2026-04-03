# 08 | 参考答案：渐进式披露原理

## 📋 基础任务参考答案

### 任务 1：Level 判断

| 内容 | 应该在哪个 Level？ | 理由 |
|------|-----------------|------|
| `name: code-review` | **Level 1** | YAML 元数据，始终加载 |
| `description: 代码审查 SOP...` | **Level 1** | YAML 元数据，始终加载 |
| 详细的安全检查清单（500字） | **Level 3** | references/，必要时加载 |
| `scripts/run-tests.sh` 执行脚本 | **Level 3** | scripts/，按需执行 |
| `references/security-checklist.md` | **Level 3** | references/，按需加载 |
| 输出报告的模板格式 | **Level 2** | SKILL.md 正文内容 |
| 触发关键词列表 | **Level 1** | 已在 description 中 |

### 任务 2：渐进式披露结构设计

```
code-review/
├── SKILL.md                      # Level 2：正文
│   ├── YAML 元数据
│   ├── When to Use
│   ├── Steps（引用外部资源）
│   └── Output Format
├── scripts/
│   └── generate-report.sh        # Level 3：生成报告脚本
└── references/
    ├── security-checklist.md     # Level 3：详细安全检查项
    ├── performance-checklist.md # Level 3：详细性能检查项
    └── output-template.md        # Level 3：输出模板
```

**SKILL.md 中的引用方式：**

```markdown
## Steps

1. 执行安全检查（见 `references/security-checklist.md`）
2. 执行性能检查（见 `references/performance-checklist.md`）
3. 运行报告脚本：`scripts/generate-report.sh`
```

### 任务 3：错误分析

**问题：**
把所有内容堆在 SKILL.md 正文里，会导致：
1. 正文过长（100+ 行 + 100+ 行 = 超过 5k tokens）
2. 每次触发都要加载全部内容，速度慢
3. 上下文被塞满，AI 难以处理

**改进方案：**
1. 把检查清单移到 `references/` 目录
2. 在 Steps 中引用：`见 references/security-checklist.md`
3. 只有实际需要时，AI 才会加载引用内容

---

## 继续学习

→ 下一章：[09 - 写好 Instructions](../concepts/09-写好Instructions.md)
