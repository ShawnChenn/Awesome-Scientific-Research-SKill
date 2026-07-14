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

## 二、原子关注点账本（Atomic Concern Ledger）— v3 增强版

将每条评论拆为不可再分的原子关注点，每条独立编号。**v3 新增字段**（来源：TobiasLee/Rebuttal-Skill）：

```yaml
concern_id: R2-W3          # Reviewer 2 第 3 条弱点
type: weakness | question | suggestion | misunderstanding
category: soundness | clarity | significance | originality | missing-baseline |
          missing-ablation | novelty | presentation | scope

# ── v3 新增：表面 vs 深层诊断（详见 deep-concern-diagnosis.md）──
surface_comment: "The gain over baseline X seems marginal."  # ≤20 词原文引用
underlying_concern: 2    # 1-12 编号（强制）
underlying_concern_secondary: null  # 可选次要深层关切
interpretation_confidence: MEDIUM  # HIGH | MEDIUM | LOW
intent_diagnosis:  # 仅当 confidence ≠ HIGH 时生成（见 deep-concern-diagnosis.md §3）
  most_likely: "Unfair comparison"
  alternative: "Statistical noise (no error bars)"
  safe_strategy: "Re-run with matched HP budget + report p-values"
sharedness: single  # all_reviewers | multiple_reviewers | single_reviewer | meta_review_or_ac
decision_impact: HIGH  # HIGH | MEDIUM | LOW

# ── 原有字段（保留）──
quote: "原文短引"
severity: critical | major | minor  # 替代旧 🔴🟡🟢
status: open | answered | deferred
```

**拆分原则：**
- 一条长评论可能含 2–3 个原子关注点，分别编号。
- 误解类（misunderstanding）单独标记，回应策略是"澄清"而非"修补"。
- 钉到出处：`[R2-W3]` 在后续所有阶段引用。
- **强制**：每条原子评论必须完成「表面评论 → 深层关切」推断（12 类选 1）。详见 `deep-concern-diagnosis.md` §2。
- 当 `interpretation_confidence ≠ HIGH` 时，必须生成意图诊断卡。详见 `deep-concern-diagnosis.md` §3。

## 三、常见关注点聚类（Cross-Reviewer Clustering）— v3 增强

将跨审稿人的同类关注点归并，识别：

| 聚类类型 | 含义 | 优先级 |
| :--- | :--- | :--- |
| **共识弱点** | ≥2 位审稿人点名 | 最高，必须正面回应 |
| **孤立点** | 仅 1 位提出 | 中，按影响评估 |
| **可快速澄清** | 误解类，一句话可解 | 高性价比 |
| **AC 点名** | AC 或元审稿提出 | 高 — 直接来自决策者 |

### v3 优先级排序公式

定性参考公式（不要求精确计算，但排名必须能用散文解释）：

```
优先级价值 ≈ 决策影响 × 共享性 × 严重性 × 预期信息增益 × 可行性 / 成本
```

产物：`.paper-rebuttal/memory/concern_ledger.json`
