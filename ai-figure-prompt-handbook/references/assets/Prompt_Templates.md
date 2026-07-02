# Prompt Templates

## Minimal Prompt

```text
Design a publication-quality research figure for [TOPIC]. The core claim is [CLAIM]. Use a clean modular layout with [LAYOUT]. Show [REGIONS]. Highlight [NOVELTY]. Use restrained semantic colors, consistent typography, clean vector graphics, and short scientific labels. Avoid clutter, tiny text, decorative effects, and literal implementation details.
```

## Full Prompt

```text
Create a publication-quality research visualization for [PAPER/TOPIC], suitable for [VENUE/USE]. The figure should communicate this claim: [CLAIM].

Canvas: [ASPECT RATIO / SINGLE COLUMN / DOUBLE COLUMN / SLIDE].
Layout: [LAYOUT PATTERN], divided into [REGIONS].
Visual hierarchy: make [MAIN CONTRIBUTION] dominant; keep [CONTEXT/BASELINES] secondary.
Flow: show [INPUT] -> [CORE MECHANISM] -> [OUTPUT/EFFECT].
Labels: [EXACT LABELS].
Color semantics: [COLOR ROLES].
Typography: modern sans-serif, clear hierarchy, short labels.
Style: clean vector graphics, modular cards, subtle dividers, consistent line weight.
Negative constraints: no dense text, no code screenshots, no generic stock imagery, no decorative gradients, no photorealistic clutter, no unreadable micro-labels.
```

## Research Media Card Prompt

```text
Design a research media card in a warm editorial science-communication style for [PAPER/TOPIC]. The card should communicate this story: [ONE-SENTENCE TAKEAWAY].

Translate the paper into a broad-audience visual narrative rather than drawing the research pipeline directly. Use multiple modular cards, each answering exactly one question: background, challenge, insight, method, why it works, evidence, and takeaway. Keep the tone academic, trustworthy, friendly, lightweight, and highly readable.

Use soft warm semantic colors with this mapping: orange for core idea, green for advantage, blue for method, red for problem, gray for background. Use a large title, three font levels only, outline icons with consistent stroke width, and lightweight conceptual metaphors such as maze, funnel, scale, road, memory box, or comparison bars. If results are shown, simplify them to trends, comparison, and conclusion only.

Include only these labels: [TEXT]. Avoid dense architecture diagrams, engineering flowcharts, code screenshots, rainbow palettes, generic robot imagery, decorative gradients, and tiny implementation details.
```
