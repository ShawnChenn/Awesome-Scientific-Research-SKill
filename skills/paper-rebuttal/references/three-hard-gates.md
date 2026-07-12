# Three Hard Gates (三大安全门控)

> 来源：wanshuiyin/Auto-claude-code-research-in-sleep (Workflow 4: Rebuttal)
> 适用：第五阶段提交前安全门禁 + 全流程每条事实/承诺/覆盖的源头控制

任何一项不通过 = **不得定稿**。三大门控贯穿全流程，每个原子关注点（ISSUE_BOARD）和每条草稿回应都必须可追溯到三大门控之一。

---

## Gate 1: Provenance（来源门）

**每条事实陈述必须映射到来源**。来源缺失 = 阻断。

| 来源类型 (`source_provenance`) | 含义 | 示例 |
| :--- | :--- | :--- |
| `paper` | 论文已发表 / 已 cite 的内容 | "Table 2 shows X" |
| `review` | 审稿人原评论 | "R2 says: 'limited baselines'" |
| `user_confirmed_result` | 用户口头/书面确认的实验 | "我跑过 Y，结果是 Z" |
| `user_confirmed_derivation` | 用户确认的推导 | "我推导过定理 3" |
| `future_work` | 计划但未完成的实验 | "We will extend to ..." |

**反例（违反）**：

- ❌ "我们的方法在 A 上比 Smith'24 高 5.2%" — 无 `source_provenance` 则阻断
- ✅ "[`user_confirmed_result`] Our method achieves 5.2% gain on A (full numbers in new Table R1)"

**补救路径**：缺来源 → 暂停问用户（"请提供：实验日志 / 表格 / 截图 / 推导笔记"）。

---

## Gate 2: Commitment（承诺门）

**每个承诺必须经批准**。未批准 = 阻断。

| 承诺类型 (`commitment`) | 含义 | 风险 |
| :--- | :--- | :--- |
| `already_done` | 实验/编辑已完成并可验证 | 低 |
| `approved_for_rebuttal` | 用户明确同意纳入 rebuttal | 中 |
| `future_work_only` | 仅作为未来工作提及，不承诺 | 低 |

### 双向约束（bidirectional）

- 草稿中每条**论文编辑承诺** → 必须出现在 `REVISION_PLAN.md`（否则违反门）
- `REVISION_PLAN.md` 每条 → 草稿中必须有对应锚点（否则违反门）

**反例**：

- ❌ 草稿承诺 "we will add a comparison with X in camera-ready" 但 REVISION_PLAN 没列 → 违反
- ❌ REVISION_PLAN 写 "Add Figure 5" 但草稿没提到 → 违反

---

## Gate 3: Coverage（覆盖门）

**每个审稿人问题必须有结论**。问题消失 = 阻断。

| 问题状态 (`status`) | 含义 |
| :--- | :--- |
| `answered` | 草稿中已回答（有锚点） |
| `deferred_intentionally` | 主动推迟到 camera-ready / 未来工作，必须有理由 |
| `needs_user_input` | 缺信息，暂停问用户 |

**关键约束**：审稿人提出的关切不能"消失"。若决定不答，必须标 `deferred_intentionally` 并说明理由：

- 已在他处答过（指向 `draft_anchor`）
- 与论文主线无关（"out of rebuttal scope"）
- 已写入 limitations 段

---

## 与现有 6 项检查的整合

三大门控**取代并扩展**现有安全门禁。前 3 项归并入三大门控，保留 3 项独立检查：

| 现有 6 项检查 | 归属 |
| :--- | :--- |
| 无支撑声明 | → **Provenance** |
| 伪造结果 | → **Provenance + Commitment** |
| 未确认权限 | → **Commitment**（保留独立检查） |
| 敌对语气 | → 保留独立检查（`tone-guidelines.md`） |
| 匿名泄漏 | → 保留独立检查 |
| 高风险表述 | → `tone-guidelines.md` 风险表达清单 |

完整 8 项最终安全门禁见 `SKILL.md` 第五阶段。

---

## 使用流程

1. **每条 ISSUE_BOARD 条目**创建时：填齐 `source_provenance` + `commitment` + `status`
2. **每条草稿回应**起草时：开头标注三标签（如 `[paper] [already_done] [answered]`）
3. **第五阶段 lint**：三大门控独立 lint 一次；任一不过即退回起草阶段
4. **REVISION_PLAN 同步**：草稿定稿前最后一步 = REVISION_PLAN 双向往返校验

---

## 反幻觉规则（hard rule）

任何新增引用必须经过：

```
DBLP 查重  →  CrossRef DOI 验证  →  [VERIFY] 标签标记已人工核验
```

未通过 DBLP/CrossRef 的引用不得加入。审稿人引用"X 方法"时，先 DBLP 搜作者+年份+标题，三者不匹配则标 `[UNVERIFIED — needs author check]`。
