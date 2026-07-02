# Paper Framework Figure

Use for main architecture, full method overview, or paper Figure 1.

## Narrative Shape

Show the full research idea as a left-to-right or top-to-bottom story:

1. Input/problem context.
2. Core proposed framework.
3. Key reasoning or learning mechanism.
4. Output/effect/evaluation signal.

## Reference Samples

When the user explicitly asks for a paper framework figure, read [Pipeline_Framework_Samples.md](Pipeline_Framework_Samples.md) for layout and structure cues.

## Prompt Skeleton

```text
Create a publication-quality framework figure for a research paper about [TOPIC]. The central scientific claim is: [CLAIM].

Use a clean modular layout with [LEFT/RIGHT/TOP/BOTTOM] flow. Divide the canvas into [N] semantic regions: [REGION LIST]. Make the proposed method visually central and larger than inputs, baselines, and outputs. Use cards, grouped modules, subtle dividers, and clear arrows to show information flow. Represent each module with simple vector icons or abstract scientific glyphs, not screenshots or code.

Include these labels exactly: [LABELS].

Use a restrained academic palette: neutral background, dark text, one primary method color, one secondary data color, and one accent color for the key contribution. Typography should be consistent, modern sans-serif, with clear hierarchy between title, module labels, and annotations. Avoid decorative complexity, tiny text, 3D effects, photorealistic objects, and crowded arrows.
```

## Design Checks

- Can a reviewer name the input, contribution, and output in 5 seconds?
- Is the proposed method visually more important than baselines?
- Are arrows few enough to read as a story rather than a wiring diagram?
