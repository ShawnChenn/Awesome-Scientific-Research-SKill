---
name: paper-rebuttal
description: >-
  投稿后 rebuttal 辅助 skill：在收到审稿意见后，规范化理解评审、规划反驳策略、起草
  格式感知的 rebuttal 回应，并在提交前过三大安全门禁（Provenance 来源门 / Commitment 承诺门
  / Coverage 覆盖门）。覆盖全生命周期：反驳可行性决策门（PROMISING/BORDERLINE/LOW_EXPECTED_RETURN）
  → 状态恢复 → 评审深层诊断（12 类 underlying concern + 意图诊断卡）→ 策略规划（P0-P3 五级
  实验优先级 + 优先级公式 + 关键审稿人识别 + 字符预算）→ 起草（Direct Answer → Evidence →
  Revision + 防御性 5 动作 + REVISION_PLAN）→ 结果整合验证 → 8 项提交前安全门禁 → 压力测试
  （5 轮硬上限）→ 多轮讨论（增量回复 + 技术升级）→ 重新提交模式（R0-R3 修订路线图）。
  支持 single_document（ICML/NeurIPS/ICLR）与 per_reviewer_thread（OpenReview）两种 venue mode。
  适用于：NeurIPS / ICLR / ACL (ARR) / ICML / 期刊 等会议的 rebuttal 阶段。
  用法示例："Use Paper-Rebuttal to initialize this rebuttal workspace."
  / "Build the concern analysis and strategy plan from reviews in Reference/."
  / "Draft a one-page PDF rebuttal from the approved strategy."
  / "Rehearse: simulate reviewers and AC, tell me what to harden."
---

# Paper-Rebuttal — 投稿后反驳辅助

技能优先架构：本 `SKILL.md` 为单一入口，串联 `references/` 下的分层原子能力文件，
覆盖从工作区初始化、状态恢复、证据收集、评审理解、策略规划、草稿撰写、提交前安全门禁到多轮
讨论的全生命周期。各阶段生成的结构化记忆持久化在 `<rebuttal-workspace>/.paper-rebuttal/`
（与 `rebuttal/` 平行）中。**所有阶段必须服从三大门控**（见 `references/three-hard-gates.md`）。

## 推荐工作区布局

在论文 rebuttal 工作区内建立如下结构（技能运行时状态存于 `.paper-rebuttal/`，制品文件存于
`rebuttal/`，二者互为镜像）：

```
<rebuttal-workspace>/
├── Code/                          # 补实验代码
├── Paper/                         # 论文源文件 / 修订版
├── Reference/                     # 审稿意见、参考文献、相关论文
├── Temp/                          # 临时草稿
├── rebuttal/                      # 制品文件（v2 命名空间）
│   ├── REBUTTAL_STATE.md          # 状态记录（支持中断恢复）
│   ├── REVIEWS_RAW.md             # 原始评审（逐字）
│   ├── ISSUE_BOARD.md             # 原子问题看板（v2 字段）
│   ├── STRATEGY_PLAN.md           # 策略计划
│   ├── REBUTTAL_DRAFT_v1.md       # 初始草稿
│   ├── REBUTTAL_DRAFT_rich.md     # 扩展版（带 [OPTIONAL] 标记）
│   ├── PASTE_READY.txt            # 严格纯文本（精确字符数）
│   ├── REVISION_PLAN.md           # 整体修订检查清单
│   ├── MCP_STRESS_TEST_round.md   # 压力测试记录
│   ├── FOLLOWUP_LOG.md            # 跟进轮次日志
│   └── Reviewer_<ID>_response.md  # 逐审稿人文件（per_reviewer_thread）
└── .paper-rebuttal/               # 技能运行时记忆（与 rebuttal/ 镜像）
    ├── memory/                    # 结构化记忆 JSON
    ├── drafts/                    # 回应草稿
    ├── snapshots/                 # 快照
    ├── templates/                 # 模板
    ├── logs/                      # 操作日志
    └── cache/                     # 缓存
```

> 制品文件结构与字段模板见 `references/phase-artefacts.md`。

## 关键常量（可被用户覆盖）

| 常量 | 默认值 | 含义 |
| :--- | :--- | :--- |
| `VENUE` | `ICML` | 目标会议/期刊 |
| `VENUE_MODE` | `single_document` | `single_document` 或 `per_reviewer_thread` |
| `RESPONSE_MODE` | `TEXT_ONLY` | v1 仅支持纯文本 |
| `QUICK_MODE` | `false` | `true` 时仅运行 Phase 0-3 后退出 |
| `AUTO_EXPERIMENT` | `false` | `true` 时启用 Phase 3.5 证据冲刺 |
| `RENDER_HTML` | `true` | `true` 时 Phase 9 自动渲染 HTML |
| `MAX_INTERNAL_DRAFT_ROUNDS` | `2` | 草稿→lint→修订循环上限 |
| `STRESS_TEST_ROUNDS_BASE` | `1` | 压力测试基础轮次 |
| `STRESS_TEST_ROUNDS_HARD_CAP` | `5` | 压力测试硬上限 |
| `MAX_FOLLOWUP_ROUNDS` | `3` | 每审稿人线程跟进轮次上限 |

**覆盖示例**：
```
Use Paper-Rebuttal with venue: NeurIPS, char limit: 5000, VENUE_MODE: per_reviewer_thread.
```

## 开工前：初始化工作区（或恢复状态）

```
Use Paper-Rebuttal to initialize this rebuttal workspace.
```

- 若 `rebuttal/REBUTTAL_STATE.md` 存在 → 从 `Last completed phase` 恢复
- 否则 → 创建 `rebuttal/`，初始化所有制品

## 各阶段读取 references 文件

| 阶段 | 必读文件 | 用途 |
| :--- | :--- | :--- |
| 0 反驳可行性决策门 | `rebut-resubmit-gate.md` | PROMISING / BORDERLINE / LOW_EXPECTED_RETURN 三级评估 |
| 1 状态恢复 / 初始化 | — | 读 `REBUTTAL_STATE.md` 或创建 |
| 2 评审深层诊断 | `review-comprehension.md` + `review-taxonomy.md` + `response-modes.md` + `deep-concern-diagnosis.md` | 原子拆分 + 10 类 taxonomy + 12 类 underlying concern + 意图诊断卡 + 共享性 |
| 3 策略规划 | `strategy-planning.md` + `response-modes.md` + `defensive-moves.md` + `tone-guidelines.md` | 姿态 + P0-P3 五级优先级 + 优先级公式 + 实验计划表 + 关键审稿人 + 字符预算 + 防御动作 |
| 4 实验分类 Triage | `strategy-planning.md` | 五级实验分类；AUTO_EXPERIMENT 时进 4.5 |
| 4.5 证据冲刺（可选） | — | 仅 `AUTO_EXPERIMENT=true` 时跑 |
| 5 起草 | `phase-artefacts.md` + `rebuttal-working-template.md` + `rebuttal-templates.md` + `defensive-moves.md` + `tone-guidelines.md` + `quality-checklist.md` | Direct Answer → Evidence → Revision 模板 + 工作草稿 + 格式适配 + 防御动作 + 语气 |
| 6 安全门禁 | `three-hard-gates.md` + `rebuttal-templates.md` + `tone-guidelines.md` + `quality-checklist.md` | 8 项检查（3 大门控 + 5 独立）+ Quality Checklist |
| 7 压力测试 | `phase-artefacts.md` | 5 轮硬上限 + pivotal 聚焦 |
| 8 多轮讨论 | `phase-artefacts.md` + `tone-guidelines.md` | FOLLOWUP_LOG + 增量回复 + 技术升级 |
| 9 最终定稿 | `phase-artefacts.md` | PASTE_READY.txt + REBUTTAL_DRAFT_rich.md |
| 10 HTML 渲染（可选） | — | 仅 `RENDER_HTML=true` 时跑 |
| * 重新提交模式 | `rebut-resubmit-gate.md` | R0-R3 修订路线图 + 保留/修改/删除表 + 故事修订 |

---

## 阶段 0：反驳可行性决策门（Rebuttal-Versus-Resubmission Gate）

入口：`Use Paper-Rebuttal: the reviews and scores are in Reference/. Assess rebuttal viability.`

> 详见 `references/rebut-resubmit-gate.md`

在规划实验之前，先评估 rebuttal 是否值得投入有限的作者时间：

1. **标准化分数范围**：确定会议/期刊、分数范围、录取线、是否允许改分/新实验
2. **三级可行性评估**：
   - `PROMISING` → 进入完整诊断 + 实验计划
   - `BORDERLINE / UNCERTAIN` → 进入诊断，但格外谨慎分配时间
   - `LOW_EXPECTED_RETURN` → 输出重新提交计划（R0-R3 修订路线图），**不进入**实验计划部分
3. **低回报时必需输出 8 项**：解释为何预期价值低 + 现在仍值得回答的问题 + 不应花时间做的事 + 重新提交诊断 + R0-R3 修订路线图 + 推荐新实验 + 声明/框架修改建议 + 目标会议建议
4. 用户可覆盖：`override: proceed with rebuttal despite LOW_EXPECTED_RETURN` → 进入 Stage 1 但标记为高风险

产物：可行性评估写入 `REBUTTAL_STATE.md`；若 LOW_EXPECTED_RETURN 则额外输出 `rebuttal/RESUBMISSION_PLAN.md`

---

## 第一阶段：评审深层诊断 — 拆分 + 分类 + 深层关切推断

入口：`Use Paper-Rebuttal: the reviews are in Reference/. Build the concern analysis.`

1. **逐字归档**到 `rebuttal/REVIEWS_RAW.md`（不简化不重写）
2. **逐个 reviewer 拆分意见** → 读取 `references/review-comprehension.md`
   - 规范化审稿人元数据：id、`reviewer_stance`（positive/swing/negative/unknown）、置信度
   - 拆为原子关注点 `[R2-W3]`，钉到 `raw_anchor`（≤20 词短引用）
3. **深层关切推断**（强制步骤）→ 读取 `references/deep-concern-diagnosis.md`
   - 每条原子评论标注 `surface_comment`（审稿人原文）→ `underlying_concern`（12 类选 1）
   - 当 `interpretation_confidence ≠ HIGH` 时生成**意图诊断卡**（最可能解读 + 替代解读 + 安全回应策略）
4. **汇总跨 reviewer 的共性 concern** → 聚类识别"共识弱点"与"孤立点"
5. **给 concern 分类** → 读取 `references/review-taxonomy.md`
   - 按 10 类打标签（v2 扩展 `theorem_rigor` + `complexity`）
   - 判严重性（critical / major / minor）
   - 填 `sharedness`（all / multiple / single / meta）和 `decision_impact`（HIGH / MEDIUM / LOW）
   - 填 `reviewer_stance` + `reviewer_priority`（standard / pivotal）
6. **初选 response_mode** → 读取 `references/response-modes.md` 决策树
7. **reviewer 之间有冲突时单独标出**，不要强行统一
8. 产物：`rebuttal/ISSUE_BOARD.md`（v3 字段完整版，含 underlying_concern + intent_diagnosis + sharedness + decision_impact）

---

## 第三阶段：策略规划 — 姿态 + P0-P3 优先级 + 预算

入口：`... and a strategy plan.`

1. **最终确定 response_mode**（每条 issue 选 7 选 1，详见 `response-modes.md`）
2. **P0-P3 五级实验优先级排序**（详见 `strategy-planning.md` §2）：
   - P0 = 现在必须做（critical/major + 共享/决策关键 + 截止前可行）
   - P1 = 如有时间则高价值（大幅增强论证，P0 之后可行）
   - P2 = 锦上添花（次要声明，不太可能改变决定）
   - P3 = 推迟到修订/重新提交（需大量资源，无法在截止前完成）
   - DO NOT RUN = 不解决深层关切或重复现有证据
   - 每个 P0/P1 实验填完整的**实验计划表**（关注点ID → 深层问题 → 最小可行协议 → 预估时间 → 结果解读 → 后备方案）
3. **识别关键审稿人**（pivotal）：立场 swing + 评分边界 / 领域高声望 / 提出 critical 关切的 negative
4. **优先级排序**：按 `决策影响 × 共享性 × 严重性 × 信息增益 × 可行性 / 成本`
5. **特定审稿人目标**：
   - R1（支持/pivotal）→ 巩固
   - R2（反对/pivotal）→ 数据驱动 + 防御动作 ≥ 2 项
   - R3（中立）→ 平衡
6. **字符预算分配**（按 `VENUE_MODE`）：
   - `single_document`：opening 10-15% / per-reviewer 75-80% / closing 5-10%
   - `per_reviewer_thread`：每线程独立；pivotal +20%
7. **面向 AC 的决策事实**（closing 段使用）
8. **读取 `defensive-moves.md`**，为 pivotal 审稿人回复预选 2-3 项防御动作
9. **读取 `tone-guidelines.md`**，提前约束语气和风险表达
10. 产物：`rebuttal/STRATEGY_PLAN.md` + 更新 `REBUTTAL_STATE.md`

---

## 第四阶段：实验分类（Triage）— P0-P3 五级

基于第三阶段策略规划中的 P0-P3 分类，将"需要补实验"的关注点写入策略矩阵：

| 级别 | 含义 | 处理 |
| :--- | :--- | :--- |
| **P0 必须做** | 不补则关键弱点无法回应 | 立即排期，最高优先级 |
| **P1 高价值** | 补则显著增强说服力 | deadline 内尽量做 |
| **P2 锦上添花** | 支持次要声明 | 成本低廉且不延误 P0/P1 时做 |
| **P3 推迟** | 需大量资源，无法在截止前完成 | 写入 limitations / 重新提交路线图 |
| **DO NOT RUN** | 不解决深层关切或重复现有证据 | 跳过，不浪费反驳期 |

### 4.5 证据冲刺（仅当 `AUTO_EXPERIMENT = true`）

> 默认 `false`——**跳过此阶段，暂停并将证据缺口呈现给用户**。

若策略计划识别需要新实验证据的 issue（标签 `response_mode: grounded_evidence` + `source_provenance: needs_experiment`）：

1. 生成迷你实验计划：跑什么（消融/基线/扩展/条件检查）+ 成功标准 + 预估 GPU 小时
2. 调用实验桥：`/experiment-bridge "rebuttal/REBUTTAL_EXPERIMENT_PLAN.md"`
3. 等待结果后更新 `ISSUE_BOARD.md`
4. 实验失败/无定论：切换 response_mode 为 `narrow_concession` 或 `future_work_boundary`，**绝不伪造正面结果**
5. 时间守卫：若预估 GPU 小时超过反驳截止时间 → 跳过并标记为人工处理

---

## 第五阶段：起草（Direct Answer → Evidence → Revision + Defensive Moves + REVISION_PLAN）

入口：`Use Paper-Rebuttal to draft a one-page PDF rebuttal from the approved strategy.`

### 5.1 起草流程

1. **读取 `references/phase-artefacts.md`**，按模板输出 `REBUTTAL_DRAFT_v1.md`
2. **读取 `references/rebuttal-working-template.md`**，按工作草稿模板输出完整工作版
3. **读取 `references/quality-checklist.md`**，按 Direct Answer → Evidence → Revision 结构撰写每条主要回应
4. **读取 `references/defensive-moves.md`**，为 pivotal 审稿人回复嵌入 ≥ 2 项防御动作：
   - 最小充分证据 / 预注册校准措辞 / 前置披露非显而易见设计选择 / 结构区分优于否认 / 让步而不放弃声明
5. **读取 `references/tone-guidelines.md`**，逐条对照改写（推荐表达 vs 避免表达）
6. **读取 `references/rebuttal-templates.md`**，按 `VENUE_MODE` 选择输出形式

### 5.2 按 VENUE_MODE 输出

- **`single_document`**：生成 `REBUTTAL_DRAFT_v1.md`（共享作者回复）+ `REVISION_PLAN.md` + 后续 `PASTE_READY.txt` 与 `REBUTTAL_DRAFT_rich.md`
- **`per_reviewer_thread`**：每个审稿人一个 `Reviewer_X_response.md`，**不**生成顶层 `REBUTTAL_DRAFT_v1.md`，可选 `SETUP_METRICS_BLOCK.md`（≤ 150 词）

### 5.3 生成 REVISION_PLAN.md

5 部分（详见 `phase-artefacts.md` §6）：

1. **Header**（论文标题、会议、字符限制、轮次）
2. **Overall Checklist**（GitHub 风格原子清单，每条映射到 `issue_id`）
3. **Grouped View**（按论文位置 / 按严重性）
4. **Commitment Summary**（already_done / approved_for_rebuttal / future_work_only 计数）
5. **Out-of-scope Log**（不触发论文修订的关切）

### 5.4 每条回应结构（Direct Answer → Evidence → Revision）

每条主要回应遵循三步骤模板（详见 `quality-checklist.md` §五）：

```
C1. 描述性标题 — [reviewer IDs]
──────────────────────────────────────────
关切：[忠实的一句话转述审稿人的深层关切]
回应：[第一句直接回答 — 同意/不同意/部分同意 + 核心论证]
证据：[结果、推导、原稿位置、表格编号]
修订：[论文中的确切更改 — "We will add X to Section Y"]
──────────────────────────────────────────
```

示例（标 v3 标签 — 含 underlying_concern + sharedness）：
```
C1. Fairness of Baseline Comparison — R1, R3
──────────────────────────────────────────
关切：Is the gain over Baseline-X due to unfair hyperparameter tuning?
回应：We agree fair comparison is critical. We re-ran all baselines
      under matched tuning budgets (Table R1).
证据：Table R1: 3 datasets × 5 baselines × matched HP budget.
      Our method still achieves +8.2% avg gain (p < 0.01, paired t-test).
修订：We will add the matched-tuning protocol to Appendix C and
      clarify this in Section 5.2.
──────────────────────────────────────────
```

### 5.5 回应排序原则

按决策关键性组织回应（详见 `quality-checklist.md` §一 Stage 4）：

1. 致命或核心技术关切（severity=critical）
2. 共享的重大关切（sharedness=multiple + severity=major）
3. 实证有效性和公平比较
4. 新颖性和定位
5. 泛化、鲁棒性
6. 范围和清晰度
7. 次要评论（severity=minor，可紧凑分组处理）

> 合并共享关切，避免按审稿人逐个重复回答。

### 5.6 语气约束（起草阶段强制）

- 不得使用对抗性或情绪化表述
- 不要把 reviewer 的误解归咎于 reviewer 能力不足，改写成"论文表述仍可更清楚地说明……"
- 不得编造实验、额外消融或人工分析结果
- 不得假装已经补完实验——区分"将补充"与"已经观察到"

---

## 第六阶段：提交前安全门禁（8 项检查 + Quality Checklist）

草稿完成后必须逐条检查，任一不过则退回修正。详见 `references/three-hard-gates.md` §"与现有 6 项检查的整合"。

### 三大门控（自动 lint）

- [ ] **Provenance（来源门）**：每条事实陈述映射到 `source_provenance ∈ {paper, review, user_confirmed_result, user_confirmed_derivation, future_work}`。无 → 阻断。
- [ ] **Commitment（承诺门）**：双向校验草稿 ↔ REVISION_PLAN 完整一致。违一即阻断。
- [ ] **Coverage（覆盖门）**：每条 issue `status ∈ {answered, deferred_intentionally, needs_user_input}`，无 `open` 残留。

### 5 项独立检查

- [ ] **敌对语气**：专业、克制、尊重？对照 `tone-guidelines.md` 避免表达清单扫描。
- [ ] **匿名泄漏**：未泄露身份、机构、未公开预印本？
- [ ] **未确认权限**：无未授权引用、未公开数据、合作者未确认内容？
- [ ] **高风险表述**：无"审稿人误解""显然""全面优于"等触发词？改写为信息性澄清。
- [ ] **Thread-local context**（仅 `per_reviewer_thread` 模式）：每审稿人文件独立可读，标记"见审稿人 X"引用自带上下文片段。

### 字符限制检查

按 `phase-artefacts.md` §10 压缩顺序：冗余 → friendly 致谢 → opening → 措辞紧凑化 → **关键回答不删**。

---

## 第七阶段：提交前压力测试（Rehearsal，5 轮硬上限）

入口：`Use Paper-Rebuttal to rehearse the rebuttal: simulate the reviewers and AC, and tell me what to harden.`

### 角色模拟（3 类）

- **reconstructed reviewer**（重构审稿人）：基于其原评论推演最可能的追问
- **independent reviewer**（独立审稿人）：以新视角找草稿薄弱点
- **AC**（领域主席）：从决策视角评估整体说服力

### 压力测试执行规则（v2）

1. **基础轮**：在完整草稿上跑一次，存 `MCP_STRESS_TEST_round_1.md`
2. **pivotal 聚焦轮**：每个 `reviewer_priority: pivotal` 审稿人单独跑一轮
3. **硬上限 5 轮**——任一审稿人回复返回无新实质性问题时终止
4. **敌对设计选择扫描**：对每个实验声明问"敌对审稿人能否发现我未披露的非显而易见设计选择？"
5. **Codex 后端**（如有）：`model: gpt-5.6-sol, config: {model_reasoning_effort: xhigh}`
6. **手动后端**（如无）：使用相同 prompt + 人工评审

产出：优先加固清单（harden list）+ 预期跟进答案库（anticipated follow-up answers）。

---

## 第八阶段：多轮讨论处理（Discussion Rounds，增量回复）

入口：`Use Paper-Rebuttal: here is Reviewer 2's follow-up reply — help me decide whether and how to respond.`

### 8.1 跟进判定（4 类决策）

| 跟进类型 | 决策 | 理由 |
| :--- | :--- | :--- |
| 误解澄清 | 必须回应 | 防止 AC 误判 |
| 新证据补足 | 必须回应 | 补完后标记 issue 为 done |
| 重复已答 | 简短确认 | "As noted in our initial rebuttal, §X..." |
| 无理要求 | 礼貌不展开 | 1 句确认 + 不再纠缠 |

### 8.2 增量回复（v2 关键规则）

- **仅起草增量回复**，非全重写
- **逐字追加**审稿人原话到 `rebuttal/FOLLOWUP_LOG.md`
- **链接到现有 issue**（`Linked to: R2-C3`）或创建新 issue
- **原地更新** `REVISION_PLAN.md`（status 流转）
- **重跑**三大门控 + tone lint

### 8.3 升级原则

- **技术升级而非修辞升级**——补实验/补引用优于"再解释一遍"
- **审稿人正确时让步**——避免在无可争辩处继续争论
- **若审稿人不可动摇且无新证据**——停止争论，1 句确认 + 转 limitations

---

## 第九阶段：最终定稿

入口：`Use Paper-Rebuttal to finalize the rebuttal.`

按 `VENUE_MODE` 输出：

### 9.1 single_document 模式

| 文件 | 用途 |
| :--- | :--- |
| `PASTE_READY.txt` | 严格纯文本，精确字符数，无 Markdown 格式，可直接粘贴 |
| `REBUTTAL_DRAFT_rich.md` | 扩展版，更多细节，标 `[OPTIONAL — cut if over limit]`，供作者手动决定 |

### 9.2 per_reviewer_thread 模式

| 文件 | 用途 |
| :--- | :--- |
| `Reviewer_<ID>_response.md` | 每审稿人独立可粘贴 |
| `SETUP_METRICS_BLOCK.md` (可选) | 复用公共段（≤ 150 词） |
| `SUPPLEMENTARY_FIG_PDF/` (可选) | 会议允许匿名图表链接时 |

### 9.3 通用刷新

- 更新 `rebuttal/REBUTTAL_STATE.md`（标记 Phase 8 完成）
- 刷新 `rebuttal/REVISION_PLAN.md`（status 全 done / 剩余 deferred）
- 呈现给用户：字符数 vs 限制、待处理 / 已批准 / 已延迟计数、剩余风险 + 需手动批准的条目

---

## 第十阶段：HTML 渲染（可选，仅 `RENDER_HTML = true`）

调用：
```
/render-html "rebuttal/REBUTTAL_DRAFT_rich.md"
```

- 输出 `rebuttal/REBUTTAL_DRAFT_rich.html`
- 嵌入源 SHA256
- 附属 `.review.json` 审查 sidecar
- **不**渲染 `PASTE_READY.txt`（按设计是精确字符数纯文本）
- **非阻塞**：失败则记录失败并视为完成

---

## 重新提交模式（Resubmission Mode）

> 详见 `references/rebut-resubmit-gate.md` §0.3
> 当 Stage 0 判定为 `LOW_EXPECTED_RETURN` 或用户明确请求时使用。

### 重新提交输出（6 项）

1. **决策诊断**：解释被拒的主要机制（核心贡献不足 / 实验不充分 / 新颖性争议 / 领域不匹配）
2. **保留/修改/删除表**：三列表格 — 哪些内容保留、哪些修改、哪些删除
3. **修订待办列表**（R0-R3）：
   - `R0` = 阻止重新提交（不解决则下一轮仍会被拒）
   - `R1` = 强烈推荐（显著提升接收概率）
   - `R2` = 提高完整性（提升论文质量但非决定因素）
   - `R3` = 可选润色（锦上添花）
4. **下次提交的实验计划**：哪些实验在反驳期内做不完但值得做
5. **故事和声明修订**：建议修订一句话贡献、摘要声明、最强有力的新颖性陈述
6. **论文结构调整**：建议对标题、摘要、引言、方法等章节的具体修改

> 不要将重新提交视为失败——在当前情况下它是更高回报的路径。

---

## 边界

- **不替用户决定接收结果**。产出供用户审阅定稿，最终回复由用户负责。
- **不伪造证据**。补实验只陈述真实结果；不可行项写入 limitations。
- **不代替与 AC/审稿人的私下沟通**。所有内容走正式 rebuttal 通道。
- **保护匿名性**。rebuttal 阶段不得泄露作者身份或未公开信息。
- **不跑新实验除非 `AUTO_EXPERIMENT=true`**。默认仅整理证据 + 起草。
- **不渲染 PDF 修订版或上传到会议系统**。用户手动完成提交。
