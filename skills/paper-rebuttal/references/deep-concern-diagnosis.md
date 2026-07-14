# Deep Concern Diagnosis（深层关切诊断 + 意图诊断卡）

> 来源：TobiasLee/Rebuttal-Skill (Stage 1.2-1.3)
> 从审稿人的表面评论推断其底层的决策疑虑，是强制步骤而非可选步骤。

---

## 1. 区分表面评论与深层关切

对每条原子评论，必须完成以下四元分析：

| 字段 | 含义 | 示例 |
| :--- | :--- | :--- |
| `surface_comment` | 审稿人原文（≤ 20 词短引用） | "The gain over baseline X seems marginal." |
| `underlying_concern` | 审稿人真正担心的决策级问题 | 方法是否只对特定设置有效？贡献是否足够？ |
| `evidence_to_resolve` | 能解决此关切的具体证据 | 多数据集上的 p-value + 效应量 |
| `interpretation_confidence` | 对该推断的确信度（HIGH/MEDIUM/LOW） | MEDIUM |

---

## 2. 12 类深层关切清单

在推断时，从以下清单中选择最匹配的深层关切（可多选，但标注主要 + 次要）：

| # | 深层关切 | 英文关键词 | 表面信号 |
| :--- | :--- | :--- | :--- |
| 1 | 方法是否正确？ | Correctness | "there seems to be an error in..." / "the derivation is unclear" |
| 2 | 增益是否来自不公平比较？ | Unfair comparison | "did you tune baselines equally?" / "missing strong baseline X" |
| 3 | 方法是否只适用于特例？ | Generality / Special case | "only tested on one dataset" / "does this work for..." |
| 4 | 贡献是否新颖？ | Novelty | "similar to [X]" / "incremental over..." |
| 5 | 任务是否重要？ | Significance / Importance | "is this task well-motivated?" / "limited practical impact" |
| 6 | 结论是否统计可靠？ | Statistical reliability | "no error bars" / "is this significant?" |
| 7 | 方法是否可扩展？ | Scalability | "how does this scale to..." / "computational cost?" |
| 8 | 方法是否可复现？ | Reproducibility | "no code" / "hyperparameters not reported" |
| 9 | 成本是否值得？ | Cost-effectiveness | "the improvement does not justify the complexity" |
| 10 | 声明是否超出证据范围？ | Claim-evidence gap | "the claim is too strong given..." / "overclaiming" |
| 11 | 审稿人因论文不清晰而困惑？ | Clarity-induced confusion | "I'm not sure I understand..." / "unclear presentation" |
| 12 | 审稿人的期望与论文贡献不符？ | Expectation mismatch | "I expected a different contribution" / "the framing is misleading" |

> **强制性**：每条原子评论都必须标注 `underlying_concern` 字段（选 1 个主要 + 可选 1 个次要）。

---

## 3. 意图诊断卡（Intent Diagnosis Card）

当审稿人意图模糊（`interpretation_confidence = LOW` 或 `MEDIUM` 且存在多个合理解读）时，生成意图诊断卡：

```
INTENT DIAGNOSIS CARD: [issue_id]
──────────────────────────────────────────
Reviewer's words:  [≤20 词原文引用]
Most likely concern: [深层关切 #N + 简短解释]
Alternative interpretation: [另一种可能的深层关切 + 为什么也可能成立]
Confidence: LOW | MEDIUM
Why uncertain: [为何无法确定 — 审稿人表述模糊 / 缺少上下文 / 与其他评论矛盾]
Evidence that resolves both: [能同时验证两种解读的实验或澄清]
Question for authors: [直接问作者的问题 — "When Reviewer 2 says X, do they mean A or B?"]
Safe response strategy: [在不确定时仍能推进的安全回应策略]
──────────────────────────────────────────
```

### 意图诊断卡的用途

- **作者澄清**：在投入实验资源之前，先确认审稿人的真实意图
- **避免浪费**：防止基于错误解读运行昂贵实验
- **安全回应**：即使作者无法确认，诊断卡也提供了「同时覆盖两种解读」的安全策略

---

## 4. 共享性维度（Sharedness）

每个关切点标注审稿人之间的重叠程度，影响优先级排序：

| 标签 | 含义 | 优先级影响 |
| :--- | :--- | :--- |
| `all_reviewers` | 所有审稿人提出 | 最高优先级 — 这是「共识弱点」 |
| `multiple_reviewers` | ≥2 位审稿人提出 | 高优先级 — 跨审稿人的共同关切 |
| `single_reviewer` | 仅 1 位审稿人提出 | 中等 — 取决于该审稿人的 pivotal 状态 |
| `meta_review_or_ac` | AC 或元审稿提出 | 高优先级 — 直接来自决策者 |

> 共享性越高 → 优先级越高（即使单个审稿人的严重性较低，若多位审稿人提出也应升优先级）。

---

## 5. 决策影响（Decision Impact）

评估解决该关切对改变审稿决定的可能性，**不等同于严重性**：

| 级别 | 含义 | 示例 |
| :--- | :--- | :--- |
| `HIGH` | 解决后极可能改变决定 | 补上核心消融、纠正关键误解 |
| `MEDIUM` | 解决后有适度帮助 | 添加更多分析、改进呈现 |
| `LOW` | 解决后不太可能改变决定 | 小格式问题、边缘引用缺失 |

> 例：一个 typo（severity=minor）可能 decision_impact=LOW；一个 reviewer 的深层怀疑（severity=major 但对单个 reviewer）可能 decision_impact=MEDIUM。

---

## 6. 与现有 Issue Board 的集成

在 `ISSUE_BOARD.md` 中，每条 issue 追加以下 v3 字段：

| 字段 | 取值 | 来源 |
| :--- | :--- | :--- |
| `surface_comment` | 字符串（≤ 20 词） | 审稿人原文 |
| `underlying_concern` | 1-12 编号 | 本节 §2 |
| `underlying_concern_secondary` | 1-12 编号（可选） | 本节 §2 |
| `interpretation_confidence` | HIGH / MEDIUM / LOW | 本节 §3 |
| `sharedness` | all / multiple / single / meta | 本节 §4 |
| `decision_impact` | HIGH / MEDIUM / LOW | 本节 §5 |
| `intent_diagnosis` | 意图诊断卡（仅当 confidence ≠ HIGH） | 本节 §3 |

示例（合并到现有 ISSUE_BOARD.md 行）：

```markdown
| ID | Rev | Surface | Underlying | Confidence | Severity | Sharedness | Decision Impact | Response Mode | ... |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| R2-C3 | R2 | "gain over baseline X seems marginal" | #2 Unfair comparison | MEDIUM | major | single | HIGH | grounded_evidence | ... |
```
