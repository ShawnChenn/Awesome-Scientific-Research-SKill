# Response Modes (7 种响应模式)

> 来源：wanshuiyin/Auto-claude-code-research-in-sleep (Phase 2)
> 适用：第二阶段策略规划，为每条 ISSUE_BOARD 条目选择响应模式

每条原子关注点必须选择**恰好一种**响应模式。模式决定起草阶段的回应结构、证据要求和风险等级。

---

## 7 种响应模式速查

| 模式 | 适用场景 | 关键句式 | 风险等级 |
| :--- | :--- | :--- | :--- |
| `direct_clarification` | 审稿人误读或表述歧义 | "We clarify that ..." | 低 |
| `grounded_evidence` | 需实验/数字证据 | "Table R1 shows ..." | 中（必须有数据） |
| `nearest_work_delta` | 新颖性争议 | "Our method differs from [Name'24] in X/Y/Z" | 中（必须命名最近工作） |
| `assumption_hierarchy` | 假设质疑 | "We separate core (A1) from technical (A2) assumptions" | 中 |
| `narrow_concession` | 局部让步 | "We acknowledge ... however ..." | 低 |
| `future_work_boundary` | 范围外请求 | "We agree this is interesting future work" | 低 |
| `structural_distinction` | "你的方法退化为 X" 类攻击 | "While X holds in limit Y, our method retains Z" | **高**（必须有机制） |

---

## 选择决策树

```
Q1: 审稿人是否理解错了？
  → 是 → direct_clarification
  → 否 → 继续

Q2: 我们有实验/数字证据吗？
  → 有 → grounded_evidence
  → 无 → 继续

Q3: 是新颖性争议吗？
  → 是 → nearest_work_delta（必须命名最接近的先前工作）
  → 否 → 继续

Q4: 审稿人是否要求理论假设更强？
  → 是 → assumption_hierarchy（核心 vs 技术分离）
  → 否 → 继续

Q5: 审稿人是否局部正确？
  → 是 → narrow_concession（窄度让步 + 保留核心）
  → 否 → 继续

Q6: 是范围外请求吗（如扩展到其他领域）？
  → 是 → future_work_boundary
  → 否 → 继续

Q7: 审稿人是否声称你的方法退化为其他方法？
  → 是 → structural_distinction（必须有具体机制，缺则改 narrow_concession）
  → 否 → 重新评估或 future_work_boundary
```

---

## 每种模式的"失败模式"与防御

| 模式 | 常见失败模式 | 防御策略 |
| :--- | :--- | :--- |
| `direct_clarification` | 越辩越像狡辩 | 引用 paper 原文佐证；附修订位置；用语克制 |
| `grounded_evidence` | 数字站不住脚 | 严格区分"已观察到" vs "将补充"；附误差棒/统计检验 |
| `nearest_work_delta` | 差异点太弱 | 必须有**机制级**差异（不只是结果）；引用对方代码确认 |
| `assumption_hierarchy` | 核心假设被攻破 | 不要过度技术化——AC 会一眼看穿；只列必要层级 |
| `narrow_concession` | 让步后声明被吞 | 明确"虽然 X，但论文贡献 Y 仍成立"；加防御性证据 |
| `future_work_boundary` | 听像推卸 | 承诺加入 limitations 段；说明技术上可行但范围外 |
| `structural_distinction` | 无机制空泛 | 缺机制 = 改用 narrow_concession |

---

## 与 ISSUE_BOARD 字段的对应

每条 ISSUE_BOARD 条目**必须**填写 `response_mode` 字段（在 Phase 2 完成）：

```yaml
- issue_id: R2-C3
  response_mode: structural_distinction   # 必填，从上述 7 选 1
  status: open
  source_provenance: paper
  commitment: approved_for_rebuttal
```

---

## 跨模式组合策略

**允许**：一个审稿人的不同关切用不同模式（按关切逐条选）。

**禁止**：一条关切用两种模式混合（"我们既澄清又让步"会让 AC 困惑）。

**例外（多段回应）**：单条关切的回应内部可分 2-3 段，但开头第一句必须**锁定**一个主模式。

**反例**：

- ❌ 同一段里既说"we clarify" 又说"we acknowledge" 又说"we will add" → AC 不知道你站哪边
- ✅ 第一段 clarify（主模式 = direct_clarification），第二段附 grounded_evidence 作为支撑

---

## 与 4 类旧姿态的对应关系

旧策略的 4 类姿态（接受并修补 / 澄清误解 / 温和反驳 / 暂不处理）可映射为：

| 旧姿态 | 新模式 |
| :--- | :--- |
| 接受并修补 | `narrow_concession` + `grounded_evidence` |
| 澄清误解 | `direct_clarification` |
| 温和反驳 | `structural_distinction` 或 `nearest_work_delta` |
| 暂不处理 | `future_work_boundary` + `deferred_intentionally` |

新模式更细化，允许更精确的策略选择。
