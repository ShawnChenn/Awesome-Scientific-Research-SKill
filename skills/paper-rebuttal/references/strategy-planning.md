# Strategy Planning — 策略规划能力

基于评审理解，推理反驳姿态、优先级与面向 AC 的决策事实。

## 一、反驳姿态矩阵（Posture Matrix）

对每类（聚类后）关注点，从四种姿态中选一：

| 姿态 | 适用场景 | 回应基调 |
| :--- | :--- | :--- |
| **接受并修补 (Accept & Fix)** | 共识弱点、确属真实问题 | "感谢指出，我们已补充 X" |
| **澄清误解 (Clarify)** | 审稿人误读原文 | "如 §4.2 所示，我们实际已说明…" |
| **温和反驳 (Polite Pushback)** | 立场差异、非硬伤 | "我们理解顾虑，但证据表明…" |
| **暂不处理 (Defer)** | 超出范围/不可行 | "作为 limitations 记录，未来工作" |

> 姿态选择须过安全门禁（不伪造、不敌对）。Defer 不得用于回避共识弱点。

## 二、优先级排序

按 **影响接收概率 × 可处理性** 排序：

```
priority = f(impact_on_decision, feasibility)
```

- 共识弱点 + 必须做实验 → P0
- 孤立点 + 高价值可选 → P1
- 误解澄清（低成本高收益）→ 提前处理
- 打磨类 → P2

## 三、特定审稿人目标（Per-Reviewer Goals）

| 审稿人 | 说服重点 | 语气 |
| :--- | :--- | :--- |
| R1（支持） | 强化其认可的贡献，确认无退坡 | 巩固 |
| R2（反对） | 正面解决其方法性质疑，给硬证据 | 直接、数据驱动 |
| R3（中立） | 消除其剩余疑虑，推动向 accept | 平衡 |

## 四、面向 AC 的决策事实（AC-Facing Decision Facts）

汇总最能影响 AC 最终决策的事实，单独成段用于全局评论：

- 共识弱点解决度（"3/3 主要顾虑已回应"）
- 补实验带来的指标增益（真实数字）
- 与同期工作的区分度澄清

产物：`.paper-rebuttal/memory/strategy_matrix.json`

---

## v2 增强：响应模式 + 关键审稿人 + 字符预算

> 来源：wanshuiyin/Auto-claude-code-research-in-sleep
> 详见 `references/response-modes.md`、`references/three-hard-gates.md`、`references/defensive-moves.md`

### 1. 7 种响应模式（取代 4 类旧姿态）

每条原子关注点必须从下列 7 模式中**恰好选一**（详见 `response-modes.md`）：

| 模式 | 替代旧姿态 | 何时用 |
| :--- | :--- | :--- |
| `direct_clarification` | Clarify | 审稿人误读 |
| `grounded_evidence` | Accept & Fix | 有实验/数字证据 |
| `nearest_work_delta` | Polite Pushback | 新颖性争议 |
| `assumption_hierarchy` | Polite Pushback | 假设质疑 |
| `narrow_concession` | Accept & Fix | 局部让步 |
| `future_work_boundary` | Defer | 范围外请求 |
| `structural_distinction` | Polite Pushback | "你的方法退化为 X" 类攻击 |

> 选择流程见 `response-modes.md` 决策树。

### 2. 关键审稿人 (Pivotal Reviewers) 资源倾斜

识别标准：

- 立场 `swing`（中立但有强意见）+ 评分边界值（如 5/6 临界）
- 领域内高声望审稿人（其投票被 AC 重视）
- 提出了"关键弱点" (severity=critical) 的 `negative` 审稿人

倾斜资源：

- 草稿字符预算 +20%
- 压力测试轮次 +1
- 必须使用 `defensive-moves.md` 中 ≥ 2 项动作（最小充分证据 + 预注册校准 + 结构区分 + 前置披露 + 窄度让步 中选 2）

### 3. 字符预算分配

#### `single_document` 模式

| 段 | 占比 | 用途 |
| :--- | :--- | :--- |
| Opening | 10-15% | 全局回应 + 致谢 + 总览贡献 |
| Per-reviewer | 75-80% | 逐审稿人编号回答 |
| Closing (Meta-reviewer) | 5-10% | 汇总：已解决 N/M、剩余 K 写 limitations、为何接受 |

#### `per_reviewer_thread` 模式

每审稿人独立预算；可选 `SETUP_METRICS_BLOCK.md`（≤ 150 词）复用公共段。

### 4. 双向 Commitment 校验

策略规划完成后，最后一步：**草稿中每条论文编辑承诺** ↔ **REVISION_PLAN.md** 双向校验。

- 草稿暗示 "we will add X" → REVISION_PLAN 必须有对应复选框
- REVISION_PLAN 列项 → 草稿必须有对应锚点

违反任一方向 = 阻断起草定稿。详见 `three-hard-gates.md` Gate 2。
