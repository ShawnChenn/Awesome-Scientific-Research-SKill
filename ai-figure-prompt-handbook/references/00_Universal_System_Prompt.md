# Universal System Prompt

Use this prompt as the foundation for all research figure design requests:

```text
Design the figure as a publication-quality research visualization with a strong emphasis on clarity, storytelling, and visual hierarchy. Instead of reproducing implementation details literally, communicate the core scientific idea through structured visual narratives. Use modular card-based layouts, consistent typography, restrained color palettes, semantic illustrations, and clean vector graphics. Every element should improve comprehension. Prioritize information hierarchy, semantic grouping, and communication efficiency over decorative complexity. The final figure should resemble professionally designed figures from top-tier ML conferences (KDD, WWW, NeurIPS, ICLR) or high-quality scientific media publications, balancing academic rigor with modern editorial aesthetics.
```

## Required Inputs

- Scientific claim: the one-sentence idea the figure must make obvious.
- Figure type: framework, method, motivation, comparison, taxonomy, pipeline, ablation, media card, poster, social cover, or cartoon concept.
- Target audience: reviewer, conference reader, lab meeting, media, or social audience.
- Output format: SVG, PDF, PPT, PNG, HTML/CSS, or image-generation prompt.
- Canvas: single-column, double-column, slide, poster, square, or widescreen.

## Universal Constraints

- Prefer structured visual narratives over literal code or architecture dumps.
- Use 3-5 major regions, each with a clear role.
- Make the main contribution visually dominant.
- Use short noun phrases for labels.
- Use semantic color, not decorative color.
- Ensure the figure can be understood when printed small.
- Avoid unnecessary shadows, glow, glossy effects, crowded arrows, tiny text, and generic AI-themed decoration.
