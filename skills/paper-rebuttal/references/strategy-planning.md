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

## 二、优先级排序 — v3 增强（P0-P3 五级 + 优先级公式）

> 来源：TobiasLee/Rebuttal-Skill (Stage 1B)
> 反驳期时间有限，必须返回排序后的实验计划，**不是无排序的愿望清单**。

### 2.1 优先级评分公式

定性参考（不要求精确计算，但排名必须能用散文解释）：

```
优先级价值 ≈ 决策影响 × 共享性 × 严重性 × 预期信息增益 × 可行性 / 成本
```

其中：
- `决策影响`：解决后改变审稿决定的可能性（HIGH=3, MEDIUM=2, LOW=1）
- `共享性`：审稿人重叠程度（all=4, multiple=3, single=1, meta=4）
- `严重性`：critical=3, major=2, minor=1
- `预期信息增益`：实验能提供多少新信息（HIGH=3, MEDIUM=2, LOW=1）
- `可行性`：截止日期前能否完成（HIGH=3, MEDIUM=2, LOW=1）
- `成本`：时间/计算/数据资源（LOW=3, MEDIUM=2, HIGH=1，低成本=高得分）

### 2.2 P0-P3 五级实验优先级

| 级别 | 标签 | 何时标记 | 示例 |
| :--- | :--- | :--- | :--- |
| **P0** | 现在必须做 | 解决 critical/major + 共享或决策关键 + 截止前可行 + 结果无论正负都可解释 + 无现有证据 | 补核心消融、公平比较关键基线 |
| **P1** | 如有时间则高价值 | 大幅增强论证 + 解决 major 单一审稿人或共享 moderate + P0 之后可行 | 扩展数据集、额外分析 |
| **P2** | 锦上添花 | 支持次要声明 + 不太可能改变决定 + 成本低廉且不延误 P0/P1 | 更多可视化、附录证明 |
| **P3** | 推迟到修订/重新提交 | 需大量工程/数据/计算/重新设计 + 无法在截止前可靠验证 + 解决低影响问题 | 新数据集收集、大规模扩展 |
| **DO NOT RUN** | 不要做 | 不能解决深层关切 + 重复现有证据 + 结果因缺少对照而无法解释 + 可能耗尽反驳期却留下重大问题未解决 | 无对照的额外数据集测试 |

### 2.3 实验计划表格式

每个 P0/P1 实验必须返回包含以下列的表：

| 列 | 内容 |
| :--- | :--- |
| `优先级` | P0 / P1 / P2 / P3 / DO NOT RUN |
| `关注点ID` | 映射到的 issue_id |
| `深层问题` | 要解决的 underlying concern |
| `提议的实验或分析` | 具体操作 |
| `为何改变决定` | 这个实验如何影响审稿决定 |
| `最小可行协议` | 最小可接受的实验设置 |
| `预估时间/成本` | 实际估算 |
| `结果解读` | 正面/负面/无定论各自意味着什么 |
| `未完成时的后备方案` | 如果实验失败或时间不够，如何回应 |

### 2.4 优先选择信息密度高的实验

一个实验同时回答多个问题（如：匹配计算量比较同时解决公平比较 + 效率两个关切）。

### 2.5 将实验与澄清分开

返回三个行动桶：
1. **现在运行**（P0 + 部分 P1）
2. **用现有证据或澄清回答**（无需新实验）
3. **推迟到修订/重新提交**（P3 + 部分 P2）

> 不要仅为展示努力而推荐实验——每个推荐的实验必须能回答具体的深层关切。

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
