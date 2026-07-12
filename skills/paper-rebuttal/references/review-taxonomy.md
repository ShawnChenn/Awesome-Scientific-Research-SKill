# Review Concern Taxonomy — 审稿关注点分类法

## 八种常见关注点类型

| 类型 | 标签 | 关键词 |
| :--- | :--- | :--- |
| **Novelty** | 创新性不足 | 增量不明显、与已有方法相似度 |
| **Technical Clarity** | 方法描述不清 | 关键设定缺失、公式推导缺步骤 |
| **Experimental Support** | 实验不充分 | 缺少 baseline / ablation / 错误分析 |
| **Evaluation Fairness** | 对比不公平 | 设置不一致、指标不匹配、未控制变量 |
| **Significance** | 价值不足 | 问题重要性或实际应用价值存疑 |
| **Positioning** | 文献定位不清 | 与相关工作关系模糊、引用覆盖不足 |
| **Limitation Scope** | 边界条件不明 | 适用范围、失败案例未说明 |
| **Writing Structure** | 写作/图表 | 可读性问题、图表不自解释、组织结构 |

## 严重性判断

| 级别 | 含义 | 处理要求 |
| :--- | :--- | :--- |
| **高** | 直接影响接收判断 | 通常需要补实验或关键澄清 |
| **中** | 不一定决定接收，但显著影响 reviewer 信心 | 需要有力澄清或部分实验 |
| **低** | 写作或表达层面的修订项 | 修改措辞即可 |

## 动作建议

| 动作 | 适用于 | 示例 |
| :--- | :--- | :--- |
| **必须补实验** | experimental_support、evaluation_fairness 中的硬缺口 | "缺少 ablation 对比 X 的贡献" |
| **优先澄清** | technical_clarity、positioning 中的模糊点 | "方法描述缺了步骤 Y，但实际已实现" |
| **承认局限** | limitation_scope 中的边界问题 | "当前版本仅测试了 Z 场景" |

> 分类时先定类型 → 再判严重性 → 最后给建议动作。三者不绑定（高严重性不一定必须补实验）。
