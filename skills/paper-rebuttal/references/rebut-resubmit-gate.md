# Rebuttal-Versus-Resubmission Gate（反驳 vs 重新提交决策门）

> 来源：TobiasLee/Rebuttal-Skill (Stage 0)
> 在规划实验之前，先评估 rebuttal 是否值得投入有限的作者时间。若回报低，建议转向重新提交。

---

## 0.1 标准化分数范围

在评估前先确定会议/期刊元数据：

| 字段 | 含义 | 示例 |
| :--- | :--- | :--- |
| `venue` | 目标会议/期刊 | NeurIPS, ICML, ACL |
| `score_range` | 分数范围 | 1-10, 1-5 |
| `score_labels` | 分数语义标签（如已知） | 5=strong accept, 4=accept, 3=weak accept... |
| `borderline` | 大致录取线 | ≥6.5/10 或 ≥3.5/5 |
| `has_ac_discussion` | 是否有 AC 讨论阶段 | true/false |
| `reviewers_can_change_score` | 审稿人能否改分 | true/false |
| `new_experiments_allowed` | 会议是否允许新实验 | true/false |

> 若信息未知，声明评估是暂定的，并建议作者确认。

---

## 0.2 评估反驳可行性（三级分类）

### `PROMISING`（有希望）

- 至少一个审稿人态度积极或分数明显高于录取线
- 负面意见集中在可回答的误解或缺失证据上
- 无致命性正确性缺陷
- 核心问题可在反驳期内解决

**动作**：进入 Stage 1 完整诊断 + 实验计划。

### `BORDERLINE / UNCERTAIN`（临界/不确定）

- 分数集中在录取线附近
- 审稿人承认优点但指出几个可修复的问题
- 审稿人意图模糊
- 一个决定性的实验或澄清可能改变局面

**动作**：进入 Stage 1，但需格外谨慎分配时间，优先做意图澄清。

### `LOW EXPECTED RETURN`（预期回报低）

触发条件（任一）：
- **所有审稿分数低于录取线**（无积极审稿人）
- 多人质疑核心前提 / 正确性 / 新颖性 / 实证有效性
- 所需证据无法在反驳期内可靠完成
- 无 pivot 审稿人（所有立场均为 negative）

**动作**：
1. 解释为何预期价值低（明确列出阻碍因素）
2. 仍可准备一份简短的专业 rebuttal 纠正事实错误
3. **生成完整的重新提交计划**（见 §0.3）
4. 不鼓励仓促的低质量实验

---

## 0.3 低回报案例的必需输出（Resubmission Plan）

当判定为 `LOW EXPECTED RETURN` 时，输出以下 8 项：

1. **解释**：为何 rebuttal 不太可能逆转结果（逐条列出阻碍因素）
2. **现在仍值得回答的问题**：哪些事实错误或误解可以现在纠正
3. **不应花时间做的事**：哪些实验/分析在反驳期内不会改变决定
4. **重新提交诊断**：被拒的主要机制是什么（核心贡献不足 / 实验不充分 / 新颖性争议 / 领域不匹配）
5. **优先级排序的修订路线图**：按 R0-R3 排列（见下文）
6. **为下次提交推荐的新实验**：哪些实验在反驳期内做不完但值得做
7. **推荐的声明、框架和写作修改**：故事如何调整
8. **建议的目标会议/期刊考虑因素**（如有足够信息）

### 重新提交优先级（R0-R3）

| 级别 | 标签 | 含义 | 示例 |
| :--- | :--- | :--- | :--- |
| `R0` | 阻止重新提交 | 不解决则下一轮仍会被拒 | 核心方法有数学错误 |
| `R1` | 强烈推荐 | 显著提升接收概率 | 补关键基线、扩展数据集 |
| `R2` | 提高完整性 | 提升论文质量但非决定因素 | 额外消融、附录证明 |
| `R3` | 可选润色 | 锦上添花 | 写作优化、更多引用 |

---

## 0.4 决策门输出格式

在首次响应的 **A 部分**输出：

```
A. REBUTTAL VIABILITY
   Classification: PROMISING | BORDERLINE | LOW_EXPECTED_RETURN
   Score distribution: [normalized]
   Strongest positive signal: [quote]
   Strongest negative signal: [quote]
   Expected value of rebuttal effort: [narrative]
   Key assumptions: [missing info declared]
   Recommendation: [proceed with Stage 1 | proceed cautiously | switch to resubmission]
```

> 若为 `LOW_EXPECTED_RETURN`，追加完整的重新提交计划（§0.3 的 8 项输出）。

---

## 与现有流程的集成

决策门嵌入在**第一阶段之前**：

- 用户首次提供审稿意见 + 分数 + 摘要时 → 先运行决策门
- 若 `PROMISING` 或 `BORDERLINE` → 进入 Stage 1（评审理解）
- 若 `LOW_EXPECTED_RETURN` → 输出重新提交计划，**不进入** Stage 1 的实验计划部分
- 用户可覆盖决策：`override: proceed with rebuttal despite LOW_EXPECTED_RETURN` → 进入 Stage 1 但标记为高风险
