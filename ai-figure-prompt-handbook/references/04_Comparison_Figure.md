# Motivation / Comparison Figure

Use for method comparisons, baseline contrasts, before/after views, trade-off summaries, qualitative result panels, or fused motivation-plus-comparison figures.

## Narrative Shape

Use aligned evidence:

1. Same input or task.
2. Baseline paths/results.
3. Proposed method path/result.
4. Key advantage callout.

## Reference Samples

When the user explicitly asks for a comparison figure that contrasts method architectures or structural variants, read [Comparison_Architecture_Samples.md](Comparison_Architecture_Samples.md).

When the user explicitly asks for a motivation or fused motivation-plus-comparison figure, read [Motivation_Comparison_Samples.md](Motivation_Comparison_Samples.md).

## Prompt Skeleton

```text
Design a comparison figure for [TASK]. Compare [BASELINES] against [PROPOSED METHOD] using a fair, aligned layout.

Use columns or rows with identical structure for each method. Keep the proposed method visually highlighted but do not distort the comparison. Use consistent icons, equal card sizes, and aligned output regions. Add one concise callout showing the key advantage: [ADVANTAGE].

Use neutral styling for baselines and one accent color for the proposed method. Include these labels: [LABELS]. Avoid exaggerated visual bias, cluttered tables, long paragraphs, and inconsistent scales.
```

## Design Checks

- Are all methods compared under the same visual conditions?
- Is the proposed advantage explicit and evidence-linked?
- Would the figure still be credible to a skeptical reviewer?
