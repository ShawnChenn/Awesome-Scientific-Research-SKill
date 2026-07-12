---
name: paper-prereview
description: >-
  投稿前自查 skill：在论文提交前模拟严谨、公正的同行评审，预测你将收到的审稿意见，
  并给出按"影响 × 成本"排序的修补清单。模拟一个内部有分歧的审稿小组
  （R1 拥护者 / R2 方法怀疑论者 / R3·AC 新意鹰派），由 AC 综合预测结局
  （Reject / Borderline / Accept），最终输出去重后的修补清单。
  每条 weakness 必须钉到具体位置（[§x / 图y / 表z / 第n段 / "原文短引"]），
  对照 ACL H1–H17 公正性防火墙过滤不正当批评，绝不脑补缺陷。
  适用于：PDF / .tex / .md / arXiv 链接 / 粘贴文本。
  两种模式：Mode A 审自己的稿（投稿前红队，默认）；Mode B 审别人的稿（当审稿人）。
  本 skill 默认聚焦 Mode A。
---

# Paper Pre-Review — 投稿前严谨、公正、有据自查

模拟**严谨且公正**的同行评审，在投稿前把草稿挑一遍 → 预测评审与结局 → 给**修补清单**。
终点是 `prereview/<paper-slug>.md`。

## 核心信条（绝不违反）

- **凡批评必有出处。** 每条 weakness 钉到具体位置（`[§x / 图y / 表z / 第n段 / "原文短引"]`），
  定位不到、但本该有的标 `⚠ MISSING`，绝不脑补。
- **绝不编造毛病。** 真没问题就说没问题，绝不为凑数硬挑。
- **🔥 过公正性防火墙。** 任何 weakness 提出前，先对照 `references/reviewing-rubric.md`
  的 **H1–H17 黑名单**：命中（如"不够新颖却不给引用""没超 SOTA""方法太简单"
  "你该多做实验 X""有局限=有缺陷"）就**删除或降级为温和建议**，绝不当硬伤。
  这条是"严谨"与"键盘喷子"的分水岭。
- **按客观标准评。** 维度、评分量表、判据一律以 `references/reviewing-rubric.md` 为准
  （蒸馏自 NeurIPS/ICLR/ACL 官方指南），不是凭个人喜好。

## 开工前必读（三份，顺序读）

1. **`references/reviewing-rubric.md`** —— 审稿的**客观标尺**：四大维度、各会议评分量表、
   Reviewer 2 必查清单、**H1–H17 公正性防火墙**、好/烂评审标准。
2. **`references/review-schema.md`** —— 产物的字段定义：单份 review 字段、weakness 三色分级、
   meta-review + fix-list 模板、质量门。
3. **`references/reviewer-personas.md`** —— 审稿人格（R1/R2/R3·AC）盯什么、什么口吻；
   以及人格如何受防火墙约束。

## 第 0 步：判模式（先做这个）

看用户的话判 Mode A 还是 Mode B：

- **Mode A（审自己）** 信号："我的草稿 / 投稿前 / 帮我挑 / 会被怎么拒 / red-team my draft / before I submit"。
- **Mode B（审别人）** 信号："帮我审这篇 / 我要审稿 / 导师让我审 / 给个评审意见"。
- 拿不准就**问一句**："这是你**自己**要投的稿（我帮你提前挑），还是**别人**的论文（你要写正式评审）？"

> 本 skill 默认聚焦 **Mode A（投稿前自查）**。Mode B 仅在用户明确要求审别人论文时启用。

---

# Mode A：投稿前自查（红队自己的草稿）

### A1. 拿到草稿，定位骨架

用户给 PDF/.tex/.md（直接读；.tex 行号好引用）、arXiv/链接（WebFetch 取正文）、或粘贴文本。
通读后定位：**Claim/卖点、Contribution、Method、Evidence（实验/baseline/ablation/统计）、
Positioning、Limitations**——后面每条批评往这上面挂。

> 只拿到摘要/链接打不开/PDF 抠不出 → **先说清卡在哪**，别用半篇硬凑。

### A2. 跑审稿小组（逐人格出 review）

照 `references/reviewer-personas.md` 逐个出结构化 review（字段见 `references/review-schema.md`）：

- **R1 拥护者**：校准"什么是真强"，防止过度自我批评。
- **R2 方法怀疑论者**：专攻 soundness，对照 rubric 第三节必查清单（弱 baseline、缺 ablation、
  混淆变量、过拟合承诺等）。
- **R3·AC 新意鹰派**：逼问相对近期工作的新颖性。

**每条 weakness 都要：出处 + 三色分级 + 过 H 列防火墙。** 人格之间别互相抄，保留分歧。

### A3. AC 综合

共识 weakness（几人都点 = 最危险）、分歧点、决定性 2–3 条、**预测结局**
（Reject / Borderline / Accept），显式标"模拟，非真实评审"。

### A4. 出修补清单（Mode A 的真正价值）

所有 weakness 去重，按**影响 × 成本**排序。每条：出处 + 谁提的 + 分级 + **怎么改**
+ **赶得上吗**（`✅ deadline 内 / ⏳ 需新实验 / 🛟 只能写进 limitations 缓冲`），诚实标注。

### A5. 过质量门

对照 `references/review-schema.md` 质量门逐条打勾（含：每条 weakness 有出处+分级？
有没有假 weakness？**有没有漏过 H 列防火墙的不正当批评？** 预测结局标了"模拟"？
fix-list 按影响×成本排序？）。

---

## 边界（两种模式都守）

- **不替用户改/写论文。** 本 skill 产诊断（修补清单），真去动草稿是另一回事。
- **不编实验数据。** 建议"补实验"时只说补什么、为什么，绝不编结果。
- **不保证录用 / 不替 AC 做决定。** 降低被毙风险 ≠ 保录；预测结局是模拟。
- **不替用户冒充。** 产出供用户审阅定稿，提醒用户对照论文核对每个 `[出处]` 后再提交。
