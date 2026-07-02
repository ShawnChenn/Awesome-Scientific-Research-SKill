---
name: ai-figure-prompt-handbook
description: Create publication-quality research figure prompts and visual specifications for AI-generated or manually designed academic figures. Use when the user asks to design, rewrite, polish, or systematize prompts for paper framework figures, motivation figures, comparison figures, training pipelines, posters, or research media cards for ML/AI/scientific papers. For paper figures such as motivation, framework, comparison, or pipeline diagrams, default to generating an editable `.drawio` file through the standalone drawio-diagram-builder skill.
---

# AI Figure Prompt Handbook

## Core Principle

Design figures as research communication artifacts, not literal screenshots of implementation details. Emphasize clarity, storytelling, hierarchy, semantic grouping, restrained color, clean vector geometry, and top-tier ML conference aesthetics.

Use this universal design prompt as the default visual standard:

> Design the figure as a publication-quality research visualization with a strong emphasis on clarity, storytelling, and visual hierarchy. Instead of reproducing implementation details literally, communicate the core scientific idea through structured visual narratives. Use modular card-based layouts, consistent typography, restrained color palettes, semantic illustrations, and clean vector graphics. Every element should improve comprehension. Prioritize information hierarchy, semantic grouping, and communication efficiency over decorative complexity. The final figure should resemble professionally designed figures from top-tier ML conferences (KDD, WWW, NeurIPS, ICLR) or high-quality scientific media publications, balancing academic rigor with modern editorial aesthetics.

## Workflow

1. Identify the figure type from the user's request.
2. Ask for missing scientific inputs only when needed: paper title, key claim, method modules, data flow, baselines, metrics, target venue, output format, and aspect ratio.
3. Load the matching reference file from `references/`.
4. Load shared assets guidance when useful:
   - `references/assets/Layout_Patterns.md` for composition.
   - `references/assets/Color_System.md` for palettes and semantic colors.
   - `references/assets/Icon_Library.md` for visual metaphors.
   - `references/assets/Typography.md` for labels and hierarchy.
   - `references/assets/Prompt_Templates.md` for reusable prompt blocks.
5. Produce a complete figure prompt with: purpose, canvas, layout, visual hierarchy, modules, text labels, color semantics, style constraints, negative constraints, and export notes.
6. If the request is for a paper figure, especially motivation, method, framework, comparison, taxonomy, or pipeline content, generate an editable `.drawio` file by handing off to `drawio-diagram-builder`.
7. If the user needs a different figure artifact, use the appropriate drawing route: SVG/HTML/CSS for editable vector diagrams, Python/matplotlib for data-driven plots, or image generation for editorial bitmap illustrations.

## Figure Type Map

- Paper framework or architecture: read `references/01_Paper_Framework_Figure.md`.
- Motivation, problem setup, gap illustration: read `references/03_Motivation_Figure.md`.
- Comparison, baseline contrast, before/after: read `references/04_Comparison_Figure.md`.
- Training, inference, data pipeline: read `references/06_Training_Pipeline_Figure.md`.
- Academic poster figure: read `references/09_Poster_Figure.md`.
- Editable draw.io diagrams or reference-image replication: use the standalone `drawio-diagram-builder` skill.

For any paper figure request in the motivation, framework, comparison, or pipeline families, default to the editable draw.io route.

Read `references/00_Universal_System_Prompt.md` when the user asks for a general-purpose system prompt, a unified handbook, or a figure style standard.

## Output Contract

Return prompts in this structure unless the user asks otherwise:

```markdown
## Figure Prompt
[Complete prompt ready to paste into an AI image/design tool]

## Layout Notes
[Canvas, regions, hierarchy, alignment, spacing]

## Text Labels
[Exact short labels to place in the figure]

## Style Constraints
[Palette, typography, line weight, icon style, negative constraints]
```

Keep label text short and scientific. Avoid decorative clutter, faux-3D effects, generic stock imagery, excessive gradients, illegible microtext, and dense implementation jargon.
