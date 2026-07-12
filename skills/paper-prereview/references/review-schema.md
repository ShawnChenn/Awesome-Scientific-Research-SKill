# Review Schema — 产物字段定义

定义单份 review、weakness 分级、Mode A 的 meta-review + fix-list 模板、质量门。

## 一、单份 Review 字段（每个审稿人格一份）

```yaml
reviewer: R1 | R2 | R3·AC   # 人格标识
summary: "一句话概括论文核心贡献"
strengths:
  - "[§x] 具体优点描述"
weaknesses:
  - id: W1
    location: "[§4.2]" | "[Table 1]" | "[第3段]" | "⚠ MISSING"
    severity: 🔴 | 🟡 | 🟢
    text: "弱点描述"
    firewall: "过 H 列检查：未命中 / 命中 Hx 已降级"
    suggestion: "怎么改"
fixable_before_deadline: ✅ | ⏳ | 🛟
```

## 二、Weakness 三色分级

| 颜色 | 含义 | 处理优先级 |
| :--- | :--- | :--- |
| 🔴 实质 | 真问题，影响接收 | 最高，优先修 |
| 🟡 误读风险 | 表述易致审稿人误读 | 中，澄清即可 |
| 🟢 打磨 | 措辞/排版/可读性 | 低，不 blocker |

## 三、Mode A 产物：Meta-Review + Fix-List

输出到 `prereview/<paper-slug>.md`：

```markdown
# Pre-Review: <paper-title>

## 模拟结局预测
**Reject / Borderline / Accept**（模拟，非真实评审）

## 共识弱点（多人点名 = 最危险）
1. [W?] [§x] 描述 — 来自 R2,R3

## 分歧点
- R1 认为 X 是贡献，R2 认为 X 存疑

## 决定性因素（2–3 条）
1. ...

## 修补清单（按 影响 × 成本 排序）
| # | 出处 | 提出者 | 分级 | 怎么改 | 赶得上? |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | [§4.2] | R2 | 🔴 | 补 ablation X | ⏳ |
| 2 | [Table 1] | R1 | 🟢 | 重排图例 | ✅ |

## 质量门自检
- [x] 每条 weakness 有出处 + 分级
- [x] 无假 weakness
- [x] 无漏过 H 列防火墙的不正当批评
- [x] 预测结局标了"模拟"
- [x] fix-list 按影响×成本排序
```

## 四、质量门（Mode A）

逐条打勾，任一不过则回到对应步骤修正：

- [ ] 每条 weakness 有出处 + 三色分级？
- [ ] 有没有假 weakness（脑补的）？
- [ ] 有没有漏过 H 列防火墙的不正当批评？
- [ ] 预测结局是否标了"模拟，非真实评审"？
- [ ] fix-list 是否按"影响 × 成本"排序？
- [ ] 每条 fix 是否标注"赶得上吗"（✅/⏳/🛟）？
