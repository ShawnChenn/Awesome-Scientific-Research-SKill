# Phase Artefact Templates (各阶段制品模板)

> 来源：wanshuiyin/Auto-claude-code-research-in-sleep (Phase 0-9)
> 适用：全流程制品文件结构，落地在 `<rebuttal-workspace>/.paper-rebuttal/` 或 `rebuttal/`

所有制品都基于三大门控（`three-hard-gates.md`）的字段：每条 ISSUE 都标 `source_provenance` + `commitment` + `status`。

---

## 1. REBUTTAL_STATE.md (Phase 0 — 状态记录，支持中断恢复)

```markdown
# REBUTTAL_STATE

- **Paper**: [title]
- **Venue**: [ICML / NeurIPS / ICLR / ACL / 期刊]
- **Char limit**: [5000]
- **Round**: [1 / 2 / follow-up]
- **VENUE_MODE**: [single_document / per_reviewer_thread]
- **RESPONSE_MODE**: [TEXT_ONLY]
- **QUICK_MODE**: [false]
- **AUTO_EXPERIMENT**: [false]
- **RENDER_HTML**: [true]
- **Last completed phase**: [Phase 5]
- **Last updated**: [ISO 8601]
- **Reviewers**: R1, R2, R3, AC
- **Pivotal reviewers**: [R2, R3]
- **Issue counts**: open=N, answered=N, deferred=N, needs_user_input=N
```

> 每次阶段推进必须更新。**支持中断后从该阶段恢复**——重运行时先读本文件。

---

## 2. REVIEWS_RAW.md (Phase 1 — 原始评审逐字记录)

```markdown
# REVIEWS_RAW

## Reviewer 1 (R1)
- **Stance**: [positive / swing / negative / unknown]
- **Confidence**: [1-5]
- **Original text**:
> [R1 原评论，逐字保留]

## Reviewer 2 (R2)
...
```

**规则**：所有审稿人原话**逐字**保留，不简化不重写。这是审稿追踪（review tracing）的基础。

---

## 3. ISSUE_BOARD.md (Phase 2 — 原子问题看板)

```markdown
# ISSUE_BOARD

## R1-C1: [短标题]
- **issue_id**: R1-C1
- **reviewer**: R1
- **round**: 1
- **raw_anchor**: "[R1 原评论短引用 ≤20 词]"
- **issue_type**: [assumptions / theorem_rigor / novelty / empirical_support / baseline_comparison / complexity / practical_significance / clarity / reproducibility / other]
- **severity**: [critical / major / minor]
- **reviewer_stance**: [positive / swing / negative / unknown]
- **reviewer_priority**: [standard / pivotal]
- **response_mode**: [direct_clarification / grounded_evidence / nearest_work_delta / assumption_hierarchy / narrow_concession / future_work_boundary / structural_distinction]
- **status**: [open / answered / deferred / needs_user_input]
- **source_provenance**: [paper / review / user_confirmed_result / user_confirmed_derivation / future_work]
- **commitment**: [already_done / approved_for_rebuttal / future_work_only]
- **draft_anchor**: [指向 REBUTTAL_DRAFT_v1.md 的章节锚点，如 "§R1-C1"]
- **notes**: [可选]

## R2-C1: ...
```

---

## 4. STRATEGY_PLAN.md (Phase 3 — 策略计划)

5 部分：

### 4.1 全局主题（2-4 个）

```markdown
## Global Themes

### Theme 1: [主题名]
- 解决共享关切: [跨审稿人共性问题]
- 关键证据: [Table/Figure/Theorem]
- 字符预算: [N 字符]

### Theme 2: ...
```

### 4.2 响应模式分配

引用每条 ISSUE 的 `response_mode`，按"模式 → 证据要求"映射到具体草稿段。

### 4.3 字符预算

```markdown
## Character Budget

### single_document 模式
- Opening: 10-15% (N chars)
- Per-reviewer: 75-80% (N chars)
- Closing for meta-reviewer: 5-10% (N chars)
- Total: ≤ 会议限制

### per_reviewer_thread 模式
- R1: ≤ N chars
- R2: ≤ N chars
- R3: ≤ N chars
- 共用 SETUP_METRICS_BLOCK: ≤ 150 词
```

### 4.4 关键审稿人 (Pivotal Reviewers)

```markdown
## Pivotal Reviewers

- **R2**: 立场 negative, 优先级 pivotal
  - 额外草稿预算: +20% 字符
  - 额外压力测试轮次: +1 轮
  - 必须使用防御性动作: ≥ 2 项
```

### 4.5 被阻断的声明 (Blocked Claims)

```markdown
## Blocked Claims

- (R2-C3) 需要 [X] 实验数据但未提供 → 暂停问用户
- (R3-C1) 引用 [Smith'24] 未通过 DBLP/CrossRef → [UNVERIFIED]
```

> 任何未解决项 → **暂停并呈现给用户**，不进入起草。

---

## 5. REBUTTAL_DRAFT_v1.md (Phase 4 — 初始草稿)

### single_document 模式

```markdown
# Rebuttal — [Paper Title]

## Opening (10-15%)
[全局回应：致谢 + 总览论文贡献 + 三大门控均通过]

## Response to Reviewer 1

### R1-C1
**[direct_clarification]** [paper] [answered]
We clarify that ...
[引用 paper §X.Y + 附修订位置]

### R1-C2
**[grounded_evidence]** [user_confirmed_result] [approved_for_rebuttal] [answered]
We have run additional experiments on ...
[Table R1 shows ...]

## Response to Reviewer 2
...

## Closing (5-10%, for meta-reviewer)
[汇总: 已解决 N/M, 剩余 K 已写 limitations, 为何接受]
```

### per_reviewer_thread 模式

每个审稿人一个独立文件 `Reviewer_X_response.md`，**不**生成顶层 `REBUTTAL_DRAFT_v1.md`：

```markdown
# Response to Reviewer 1 (R1)

## R1-C1
[同上结构]

## R1-C2
[同上结构]
```

**关键约束**（仅 per_reviewer_thread 模式）：

- 每文件必须**独立可读**（不依赖其他审稿人文件）
- 标记 "见审稿人 X" 引用必须显式带上下文片段
- 可选 `SETUP_METRICS_BLOCK.md` 复用公共段（≤ 150 词）

---

## 6. REVISION_PLAN.md (Phase 4 — 整体修订检查清单)

5 部分：

```markdown
# REVISION_PLAN

## Header
- Paper: [title]
- Venue: [name]
- Char limit: [N]
- Round: [N]

## Overall Checklist
- [ ] (R1-C2) Add assumption hierarchy table to Section 3.1 — commitment: approved_for_rebuttal — owner: author — status: pending
- [ ] (R2-C1) Clarify novelty delta vs. Smith'24 in Section 2 related work — commitment: already_done — status: verify wording
- [ ] (R3-C4) Add runtime breakdown figure to Appendix B — commitment: future_work_only — status: deferred, note in camera-ready

## Grouped View

### By paper location
- Section 2: R2-C1
- Section 3.1: R1-C2
- Appendix B: R3-C4

### By severity
- critical: R1-C2
- major: R2-C1, R3-C4
- minor: -

## Commitment Summary
- already_done: N
- approved_for_rebuttal: N
- future_work_only: N

## Out-of-scope Log
- (R2-C5) requested new dataset — out of rebuttal scope, future work
```

**强制规则**：

- 每条清单项必须映射到 `ISSUE_BOARD.md` 的 `issue_id`
- 草稿暗示的每条论文编辑必须出现在清单（否则违反 Commitment Gate）
- 永不加无草稿或用户确认证据支撑的项
- 重运行/跟进轮次时**原地**更新复选框状态

---

## 7. MCP_STRESS_TEST_round.md (Phase 6 — 压力测试记录)

```markdown
# Stress Test Round [N]
- **Backend**: [codex / manual]
- **Model**: [gpt-5.6-sol / manual]
- **Config**: {model_reasoning_effort: xhigh}
- **Date**: [ISO]

## Inputs (with SHA256)
- REVIEWS_RAW.md: sha256:xxxx
- ISSUE_BOARD.md: sha256:xxxx
- REBUTTAL_DRAFT_v1.md: sha256:xxxx

## Findings
1. Unanswered concerns: [...]
2. Unsupported claims: [...]
3. Risky promises: [...]
4. Tone issues: [...]
5. Backfire paragraph: [...]

## Verdict
- [safe to submit / needs revision]
```

**硬上限 5 轮**。每轮保存一份。基础轮 + 每个 pivotal 审稿人 1 轮聚焦。

---

## 8. FOLLOWUP_LOG.md (Phase 8 — 跟进轮次日志)

```markdown
# FOLLOWUP_LOG

## Round 2 — [ISO date]

### R2 follow-up:
"[R2 原评论短引用，逐字]"

- **Linked to**: R2-C3 (existing) or NEW R2-C6
- **Decision**: respond (incremental) / no-response (already addressed)
- **Draft anchor**: §R2-C3-r2
- **REVISION_PLAN update**: (R2-C3) status in_progress → done
- **Lint re-run**: ✓ Coverage ✓ Provenance ✓ Commitment
```

**规则**：

- 逐字追加审稿人原话
- 仅起草**增量回复**（非全重写）
- 原地更新 REVISION_PLAN
- 重跑三大门控 + tone lint

---

## 9. 最终输出文件

### single_document 模式

| 文件 | 用途 |
| :--- | :--- |
| `PASTE_READY.txt` | 严格版本，纯文本，精确字符数，无 Markdown 格式，可直接粘贴 |
| `REBUTTAL_DRAFT_rich.md` | 扩展版本，更多细节，标 `[OPTIONAL — cut if over limit]`，供作者手动决定 |

### per_reviewer_thread 模式

| 文件 | 用途 |
| :--- | :--- |
| `Reviewer_<ID>_response.md` | 每审稿人独立可粘贴 |
| `SETUP_METRICS_BLOCK.md` (可选) | 复用公共段 |
| `SUPPLEMENTARY_FIG_PDF/` (可选) | 会议允许匿名图表链接时 |

### 两种模式通用

- `REBUTTAL_STATE.md` (刷新)
- `REVISION_PLAN.md` (刷新)
- `REBUTTAL_DRAFT_rich.html` (Phase 9, RENDER_HTML=true 时)
- `REBUTTAL_DRAFT_rich.review.json` (HTML 渲染审查 sidecar)

---

## 10. 字符超限压缩顺序（硬规则）

超限时按下列优先级压缩，**绝不删除关键回答**：

1. 冗余段（同议题在 opening/closing 重复）→ 删
2. "Friendly reviewer" 致谢段（如果字符不够）→ 压缩
3. Opening 致谢段 → 压缩到 1-2 句
4. 措辞紧凑化（不删内容，只删废话）
5. **关键回答不删**——若必须删则删除次要关切（severity=minor）
