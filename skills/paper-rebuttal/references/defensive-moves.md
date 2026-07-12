# Reviewer-Defensive Moves (5 项防御性写作动作)

> 来源：wanshuiyin/Auto-claude-code-research-in-sleep (Phase 4)
> 适用：第四阶段起草，针对敌对审稿人的"最小充分证据 + 防御性前置披露"组合

每个动作独立可用；敌对审稿人回复中**至少使用 1 项**，**关键审稿人 (`reviewer_priority: pivotal`) 回复**建议使用 2-3 项。

---

## 1. 最小充分证据 (Minimum Sufficient Evidence)

每个关切只给**最少量、但直接对应该审稿人诉求**的证据锚点。

| ❌ 反例 | ✅ 正例 |
| :--- | :--- |
| 堆砌 5 个数字试图证明一切（字符超限 + AC 厌烦） | "For R2's concern on noise robustness, Table R1 (Appendix C.2) shows 2.3% drop at σ=0.1." |

**原则**：1 个数字 > 1 段散文。审稿人问 A 就答 A，不要"顺便"也答 B/C/D。

---

## 2. 预注册校准措辞 (Pre-registration Calibration Wording)

仅在**实际为真**时使用——若阈值/留出集在检查任何生成样本前已固定：

- 明确说出 *"set on hold-out before any generated sample was inspected"*
- 或 *"frozen on validation set prior to model selection"*
- 或 *"the threshold τ=0.5 was selected on the dev set, prior to test evaluation"*

这是抵御"cherry-picking"指控的**强证据**。

❌ **不真实就绝对不要用**——审稿人一旦核实会立刻翻车，且无法补救。

---

## 3. 前置披露非显而易见设计选择 (Pre-disclose Non-obvious Design Choices)

对每个实验声明问：

> **"敌对审稿人能否发现我未披露的非显而易见设计选择？"**

若有，在 Setup 段加一行 caveat。常见需要披露的：

- 计算匹配 ≠ 轮次匹配（"FLOPs matched, not iterations"）
- 异常种子协议（"only 3 seeds due to compute limit; std in Appendix"）
- 受限参数子集（"we tuned α ∈ {0.1, 1, 10} due to budget"）
- 异常评价协议（"following Smith'24's protocol, not the standard one"）
- 数据预处理差异（"we apply [X] as in [Cite], not the default"）

**原理**：主动披露 = 主动消除攻击面。比等审稿人问出来再辩解强 10 倍。

---

## 4. 结构区分优于否认 (Structural Distinction over Denial)

当审稿人声称**"你的方法退化为 X"**或**"可被通用框架覆盖"**时：

**不要直接否认**——按 `structural_distinction` 响应模式（见 `response-modes.md`）：

1. 同意局部退化：*"We agree that in the limit X, our method reduces to Y."*
2. 展示保留的结构特征 X'/Y'/Z' 框架**无法**捕获
3. 配以具体机制：定理依赖 / 推导步骤 / 经验后果

❌ **无具体机制不用此动作**——空泛否认只会被反问 "Can you give a concrete example where Y fails on Z?" 然后哑口无言。

**反例 vs 正例**：

| ❌ 否认型 | ✅ 结构区分型 |
| :--- | :--- |
| "Our method is fundamentally different from [Smith'24]." | "While both methods share the loss formulation in Eq. 3, our method's structural prior (Theorem 2) ensures the recovered matrix has rank ≤ k, which [Smith'24] does not guarantee (see their Appendix B for counterexample). Empirically, Table R2 shows 12% gain on low-rank regime." |

---

## 5. 让步而不放弃声明 (Concede without Abandoning Claims)

当审稿人**局部正确**时：

- 明确接受：*"We acknowledge that the gain on dataset A is modest (1.2%)."*
- 然后陈述什么**仍为真**以及**为何仍支持论文贡献**
- 不必全盘接受；接受局部观点 ≠ 放弃核心贡献

**反例 vs 正例**：

| ❌ 让步过度型 | ✅ 让步有度型 |
| :--- | :--- |
| "You are right, our method has no advantage over X." | "While the gap on A is narrow (1.2%), on the other 4 datasets our method shows consistent gains (3-7%), supporting the general claim that the proposed prior is broadly beneficial." |

**规则**：每条 `narrow_concession` 必须**接续一句核心声明**——不让步吞噬论文。

---

## 强制规则 (hard rules)

- ❌ 绝不编造实验、数字、推导、引用或链接
- ❌ 绝不承诺用户未批准的
- ❌ 绝不假装已经补完实验——区分"将补充" vs "已经观察到"
- ✅ 若无强证据，**少说不多说**——沉默优于胡扯
- ✅ 每条关键审稿人回复中至少出现上述 5 个动作中的 1-2 个
