---
name: paper-rebuttal
description: >-
  投稿后 rebuttal 辅助 skill：在收到审稿意见后，规范化理解评审、规划反驳策略、起草
  格式感知的 rebuttal 回应，并在提交前过安全门禁（阻止无支撑声明、伪造结果、敌对语气、
  匿名泄漏）。覆盖全生命周期：工作区初始化 → 评审理解 → 策略规划 → 实验分类（Triage）
  → 起草 → 提交前压力测试 → 多轮讨论处理。
  支持单页 PDF、OpenReview 风格逐审稿人回复、全局评论、混合回应、Markdown+LaTeX。
  适用于：NeurIPS / ICLR / ACL (ARR) / 期刊 等会议的 rebuttal 阶段。
  用法示例："Use Paper-Rebuttal to initialize this rebuttal workspace."
  / "Build the concern analysis and strategy plan from reviews in Reference/."
  / "Draft a one-page PDF rebuttal from the approved strategy."
  / "Rehearse: simulate reviewers and AC, tell me what to harden."
---

# Paper-Rebuttal — 投稿后反驳辅助

技能优先架构：本 `SKILL.md` 为单一入口，串联 `references/` 下的分层原子能力文件，
覆盖从工作区初始化、证据收集、评审理解、策略规划、草稿撰写、提交前安全门禁到多轮讨论的
全生命周期。各阶段生成的结构化记忆持久化在 `<rebuttal-workspace>/.paper-rebuttal/` 中。

## 推荐工作区布局

在论文 rebuttal 工作区内建立如下结构（技能运行时状态存于 `.paper-rebuttal/`）：

```
<rebuttal-workspace>/
├── Code/          # 补实验代码
├── Paper/         # 论文源文件 / 修订版
├── Reference/     # 审稿意见、参考文献、相关论文
├── Temp/          # 临时草稿
└── .paper-rebuttal/
    ├── memory/        # 结构化记忆 JSON
    ├── drafts/        # 回应草稿
    ├── snapshots/     # 快照
    ├── templates/     # 模板
    ├── logs/          # 操作日志
    └── cache/         # 缓存
```

## 开工前：初始化工作区

```
Use Paper-Rebuttal to initialize this rebuttal workspace.
```

建立 `.paper-rebuttal/` 目录结构与初始记忆骨架。

## 各阶段读取 references 文件

在对应阶段必须读取以下文件（来自 `references/`）：

| 阶段 | 必读文件 | 用途 |
| :--- | :--- | :--- |
| 0 初始化 | — | 建立工作区 |
| 1 评审理解 | `review-comprehension.md` + `review-taxonomy.md` | 原子拆分 + 八类分类法 |
| 2 策略规划 | `strategy-planning.md` + `tone-guidelines.md` | 姿态矩阵 + 语气约束 |
| 3 实验分类 | `strategy-planning.md` | Triage 四类判断 |
| 4 起草 | `rebuttal-templates.md` + `rebuttal-working-template.md` + `tone-guidelines.md` | 格式模板 + 语气检查 |
| 5 安全门禁 | `rebuttal-templates.md` | 五项检查表 |
| 6 压力测试 | — | 角色模拟演练 |
| 7 多轮讨论 | `tone-guidelines.md` | 一致性 + 语气维护 |

## 第一阶段：评审理解 — 拆分 + 分类

入口：`Use Paper-Rebuttal: the reviews are in Reference/. Build the concern analysis.`

1. **逐个 reviewer 拆分意见** → 读取 `references/review-comprehension.md`
   - 规范化审稿人元数据：id、立场（支持/中立/反对）、置信度
   - 拆为原子关注点 `[R2-W3]`，钉到出处
2. **汇总跨 reviewer 的共性 concern** → 聚类识别"共识弱点"与"孤立点"
3. **给 concern 分类** → 读取 `references/review-taxonomy.md`
   - 按八类打标签：`novelty` / `technical_clarity` / `experimental_support` / `evaluation_fairness` / `significance` / `positioning` / `limitation_scope` / `writing_structure`
   - 判严重性（高/中/低）+ 建议动作（必须补实验 / 优先澄清 / 承认局限）
4. **reviewer 之间有冲突时单独标出**，不要强行统一
5. 产物：`.paper-rebuttal/memory/concern_ledger.json`

## 第二阶段：策略规划 — 姿态 + 优先级

入口：`... and a strategy plan.`

1. **反驳姿态推理**：对每类关注点决定姿态——接受并修补 / 澄清误解 / 温和反驳 / 暂不处理
2. **优先关注点**：按"影响接收概率 × 可处理性"排序
3. **特定审稿人目标**：R1（巩固）| R2（数据驱动）| R3（平衡）
4. **面向 AC 的决策事实**：汇总最能影响 AC 决策的事实（实验增益、共识解决度）
5. **读取 `tone-guidelines.md`**，提前约束语气和风险表达
6. 产物：`.paper-rebuttal/memory/strategy_matrix.json`

## 第三阶段：实验分类（Triage）

将"需要补实验"的关注点分为四类，写入策略矩阵：

| 类别 | 含义 | 处理 |
| :--- | :--- | :--- |
| **必须做 (Must)** | 不补则关键弱点无法回应 | 立即排期 |
| **高价值可选 (High-value)** | 补则显著增强说服力 | deadline 内尽量做 |
| **不推荐 (Not advised)** | 边际收益低或引新风险 | 用已有证据回应 |
| **不可行 (Infeasible)** | 时间/资源/权限不足 | 写入 limitations 缓冲 |

## 第四阶段：起草（Format-Aware Drafting）

入口：`Use Paper-Rebuttal to draft a one-page PDF rebuttal from the approved strategy.`

1. **读取 `references/rebuttal-working-template.md`**，按模板输出完整工作草稿：
   - 输入覆盖范围 → 总体判断 → 审稿意见拆分 → Concern 分类表 → 必须补实验 / 澄清 / 承认局限 → 回复策略 → Rebuttal 草稿 → **高风险表述提醒**
2. **读取 `references/tone-guidelines.md`**，逐条对照语气指南改写：
   - 推荐表达 vs 避免表达
   - 改写原则：情绪防御→信息澄清 / 绝对化→限定 / 承诺→计划 / 归咎→改进
3. **读取 `references/rebuttal-templates.md`**，按会议选择格式：
   - 单页 PDF / OpenReview 风格 / 全局评论 / 混合回应 / MD+LaTeX
4. 每条回应结构：`[定位关注点] → [姿态] → [证据/澄清] → [指向论文修订位置]`

### 语气约束（起草阶段强制）

- 不得使用对抗性或情绪化表述
- 不要把 reviewer 的误解归咎于 reviewer 能力不足，改写成"论文表述仍可更清楚地说明……"
- 不得编造实验、额外消融或人工分析结果
- 不得假装已经补完实验——区分"将补充"与"已经观察到"

## 第五阶段：提交前安全门禁（Safety Gate）

草稿完成后必须逐条检查，任一不过则退回修正。同时出具"高风险表述提醒"对照 `tone-guidelines.md` 的避免表达逐条扫描：

- [ ] **无支撑声明**：每条 claim 是否都有证据（实验/引用/推导）？无则删或补。
- [ ] **伪造结果**：绝不编造实验数据或指标；补实验只写真实结果。
- [ ] **未确认权限**：是否涉及未授权引用、未公开数据、合作者未确认内容？
- [ ] **敌对语气**：是否专业、克制、尊重？对照 `tone-guidelines.md` 避免表达清单扫描。
- [ ] **匿名泄漏**：是否意外泄露身份、机构、未公开预印本？
- [ ] **高风险表述**：有无"审稿人误解""显然""全面优于"等触发词？改写为信息性澄清。

## 第六阶段：提交前压力测试（Rehearsal）

入口：`Use Paper-Rebuttal to rehearse the rebuttal: simulate the reviewers and AC, and tell me what to harden.`

用开箱即用的角色模拟提示进行演练：

- **reconstructed reviewer**（重构审稿人）：基于其原评论推演最可能的追问。
- **independent reviewer**（独立审稿人）：以新视角找草稿薄弱点。
- **AC**（领域主席）：从决策视角评估整体说服力。

产出：优先加固清单（harden list）+ 预期跟进答案库（anticipated follow-up answers）。

## 第七阶段：多轮讨论处理（Discussion Rounds）

入口：`Use Paper-Rebuttal: here is Reviewer 2's follow-up reply — help me decide whether and how to respond.`

- 判定是否回应：误解澄清 / 新证据补足 → 回应；重复已答 / 无理要求 → 简短确认或礼貌不展开。
- 保持与首轮回应一致，不矛盾、不泄露新信息。

## 边界

- **不替用户决定接收结果**。产出供用户审阅定稿，最终回复由用户负责。
- **不伪造证据**。补实验只陈述真实结果；不可行项写入 limitations。
- **不代替与 AC/审稿人的私下沟通**。所有内容走正式 rebuttal 通道。
- **保护匿名性**。rebuttal 阶段不得泄露作者身份或未公开信息。
