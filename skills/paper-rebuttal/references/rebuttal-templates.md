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

---

## 七、Venue Mode 适配（v2 新增）

按会议格式选择：

| `VENUE_MODE` | 适用会议 | 输出形式 |
| :--- | :--- | :--- |
| `single_document` | ICML / NeurIPS / ICLR / 多数期刊 | 一份共享 `REBUTTAL_DRAFT_v1.md` + 草稿分段 |
| `per_reviewer_thread` | OpenReview 部分会议、ACM 格式 | 每审稿人独立 `Reviewer_X_response.md` |

**per_reviewer_thread 模式额外约束**：

- 每文件**独立可读**，不依赖其他审稿人文件
- 标记 "见审稿人 X" 引用必须显式带上下文片段
- 可选 `SETUP_METRICS_BLOCK.md`（≤ 150 词）复用公共段
- 第八阶段 lint 增 **Thread-local context** 检查项

---

## 八、最终输出文件（v2 新增）

### single_document 模式

| 文件 | 用途 |
| :--- | :--- |
| `PASTE_READY.txt` | 严格版本，纯文本，精确字符数，无 Markdown 格式，可直接粘贴 |
| `REBUTTAL_DRAFT_rich.md` | 扩展版本，更多细节，标 `[OPTIONAL — cut if over limit]`，供作者手动决定 |

### per_reviewer_thread 模式

| 文件 | 用途 |
| :--- | :--- |
| `Reviewer_<ID>_response.md` | 每审稿人独立可粘贴 |
| `SETUP_METRICS_BLOCK.md` (可选) | 复用公共段 |
| `SUPPLEMENTARY_FIG_PDF/` (可选) | 会议允许匿名图表链接时 |

完整制品模板见 `phase-artefacts.md`。

---

## 九、字符超限压缩顺序（硬规则）

超限时按下列优先级压缩，**绝不删除关键回答**：

1. 冗余段（同议题在 opening/closing 重复）→ 删
2. "Friendly reviewer" 致谢段（如果字符不够）→ 压缩
3. Opening 致谢段 → 压缩到 1-2 句
4. 措辞紧凑化（不删内容，只删废话）
5. **关键回答不删**——若必须删则删除次要关切（severity=minor）

---

## 十、与三大门控的集成

完整安全门禁已升级为 8 项（详见 `three-hard-gates.md`）：

| 旧 6 项 | 归属（v2） |
| :--- | :--- |
| 无支撑声明 | → Provenance |
| 伪造结果 | → Provenance + Commitment |
| 未确认权限 | → Commitment |
| 敌对语气 | 保留（`tone-guidelines.md`） |
| 匿名泄漏 | 保留 |
| 高风险表述 | `tone-guidelines.md` 风险表达清单 |

8 项最终检查 = 三大门控（Provenance/Commitment/Coverage）+ 3 项独立检查（敌对语气/匿名泄漏/未确认权限）+ 1 项风格检查（高风险表述）+ 1 项覆盖特定模式的 `Thread-local context`（per_reviewer_thread 模式）。
