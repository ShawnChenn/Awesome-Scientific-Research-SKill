---
name: research-media-card
description: Create warm editorial research media-card infographics that translate a paper into a broad-audience visual story. Use when the user explicitly asks for a research media card, science communication infographic, paper teaser card, or social-friendly card-style research summary that should not draw the pipeline directly.
---

# Research Media Card v1.0

## Core Principle

Translate the paper into a visual story for non-specialist readers. Do not draw the research pipeline directly. Prioritize narrative, conceptual illustrations, semantic grouping, and communication efficiency over implementation details.

Use the media-card prompt as the default visual standard:

> Design the figure as a research media infographic card instead of a conventional academic framework figure. The goal is to communicate a research idea to a broad audience within 10–20 seconds, allowing readers to quickly understand the problem, the core idea, the key innovation, and the take-away, without reading the paper. Organize the figure as a complete story rather than a process. Divide the page into multiple visual cards; each card should represent exactly one idea. Use a card-based editorial layout with a warm, modern, magazine-like aesthetic. Prefer simple explanatory illustrations instead of complicated architecture. Use soft semantic colors, outline icons, generous whitespace, and short labels. Do not reproduce the research pipeline directly.

## Workflow

1. Ask for the paper topic, one-sentence takeaway, and any must-include labels.
2. Map the story into 5-8 cards: title, takeaway, background, core insight, method, why it works, evidence, final takeaway.
3. Read `references/examples/Research_Media_Card_Examples.md` for layout, tone, and density when the user explicitly wants a research media card.
4. Use the shared style references when needed:
   - `references/Layout_Patterns.md`
   - `references/Color_System.md`
   - `references/Icon_Library.md`
   - `references/Typography.md`
   - `references/Prompt_Templates.md`
5. Return a complete prompt with layout notes, labels, style constraints, and negative constraints.

## Output Contract

Return prompts in this structure unless the user asks otherwise:

```markdown
## Figure Prompt
[Complete prompt ready to paste into an AI image/design tool]

## Layout Notes
[Canvas, regions, hierarchy, spacing]

## Text Labels
[Exact short labels to place in the figure]

## Style Constraints
[Palette, typography, icon style, negative constraints]
```

## Non-Negotiable Rule

Do not draw the research pipeline directly. Instead, redesign the paper into a visual story for science communication. Every visual element should exist to improve comprehension rather than faithfully reproduce the model architecture.
