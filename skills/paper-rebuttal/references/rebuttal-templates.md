# Rebuttal Templates — 回应模板与格式

提交前安全门禁 + 各格式回应模板。

## 一、安全门禁检查表（提交前必过）

逐条打勾，任一不过则退回修正：

- [ ] **无支撑声明**：每条 claim 有证据（实验/引用/推导）？无则删或补。
- [ ] **伪造结果**：无编造实验数据或指标；补实验只写真实结果。
- [ ] **未确认权限**：无未授权引用、未公开数据、合作者未确认内容？
- [ ] **敌对语气**：专业、克制、尊重？无防御性/攻击性措辞？
- [ ] **匿名泄漏**：无身份、机构、未公开预印本泄露？

## 二、单条回应结构（所有格式通用）

```
[定位] 感谢 Reviewer X 提出 [关注点 R?-W?]。
[姿态] 我们 [接受并修补 / 澄清 / 温和反驳 / 暂不处理]。
[证据] [实验增益 Δ=+Y% | 如 §4.2 所示 | 引用 Z]。
[指向] 修订已体现于 [Paper §3.1 / Appendix C / 新 Table 2]。
```

## 三、OpenReview 风格（逐审稿人 Comment）

```
Dear Reviewer X,

Thank you for your thoughtful review. We address each concern below.

**Concern [R?-W?]: <一句话>**
<按通用结构回应>

**Concern [R?-W?]: <一句话>**
<回应>

We hope these revisions address your concerns.
```

## 四、全局评论（Meta / AC Comment）

```
Summary of Changes:
- 补充了 X 实验（Δ=+Y%），回应 R2-W1, R3-W2
- 澄清了 Z 的定位误解，回应 R1-W3
- 修订稿件 §3.1 重写，Appendix C 新增

All three primary concerns raised by reviewers have been directly addressed.
```

## 五、单页 PDF（LaTeX 模板位置）

模板见 `assets/one-page-rebuttal-template/`（LaTeX 单页反驳模板）。
用于 NeurIPS 等限制单页的会议。结构：左栏逐审稿人、右栏全局 summary。

## 六、Markdown + LaTeX（通用可读版）

用于本地协作、导师审阅。支持 `$...$` 公式与表格，导出 PDF 前再过一次安全门禁。
