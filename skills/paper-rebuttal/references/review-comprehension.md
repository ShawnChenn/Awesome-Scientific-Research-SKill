# Review Comprehension — 评审理解能力

将原始审稿意见规范化为可操作的结构化记忆。

## 一、审稿人元数据 schema

```yaml
reviewer_id: R1 | R2 | R3 | AC
stance: support | neutral | oppose   # 整体立场
confidence: 1-5                       # 审稿人自报置信度
key_claims:                           # 审稿人最核心的判断
  - "主要贡献 X 有潜力"
  - "但实验不足以支撑 claim Y"
```

## 二、原子关注点账本（Atomic Concern Ledger）

将每条评论拆为不可再分的原子关注点，每条独立编号：

```yaml
concern_id: R2-W3          # Reviewer 2 第 3 条弱点
type: weakness | question | suggestion | misunderstanding
category: soundness | clarity | significance | originality | missing-baseline |
          missing-ablation | novelty | presentation | scope
quote: "原文短引"
interpretation: "审稿人真实在问什么"
severity: 🔴 | 🟡 | 🟢
status: open | answered | deferred
```

**拆分原则：**
- 一条长评论可能含 2–3 个原子关注点，分别编号。
- 误解类（misunderstanding）单独标记，回应策略是"澄清"而非"修补"。
- 钉到出处：`[R2-W3]` 在后续所有阶段引用。

## 三、常见关注点聚类（Cross-Reviewer Clustering）

将跨审稿人的同类关注点归并，识别：

| 聚类类型 | 含义 | 优先级 |
| :--- | :--- | :--- |
| **共识弱点** | ≥2 位审稿人点名 | 最高，必须正面回应 |
| **孤立点** | 仅 1 位提出 | 中，按影响评估 |
| **可快速澄清** | 误解类，一句话可解 | 高性价比 |

产物：`.paper-rebuttal/memory/concern_ledger.json`
