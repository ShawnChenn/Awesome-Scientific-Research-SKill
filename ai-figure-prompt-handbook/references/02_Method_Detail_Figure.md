# Method Detail Figure

Use for internal modules, algorithm steps, attention mechanisms, loss design, memory banks, agent loops, or model components.

## Narrative Shape

Zoom into one core module. Use progressive disclosure:

1. Context entering the module.
2. Internal operations grouped into 2-4 stages.
3. Mathematical or algorithmic signal.
4. Output returned to the larger system.

## Prompt Skeleton

```text
Design a detailed method figure that explains [MODULE NAME] in [PAPER/METHOD]. The figure should focus on mechanism, not implementation syntax.

Use a zoom-in layout: a small context strip shows where the module sits in the overall framework, and the main area explains the internal stages. Arrange the stages as [CHAIN / LOOP / STACK / PARALLEL BRANCHES]. Use compact cards for operations, thin arrows for data flow, and small equation callouts only for essential mathematical signals.

Show these stages: [STAGES]. Highlight the key novelty: [NOVELTY].

Use consistent line weights, aligned cards, minimal icons, and short labels. Make repeated tensors or tokens visually consistent with color-coded chips. Avoid pseudo-code blocks unless the algorithm itself is the contribution.
```

## Design Checks

- Does each internal stage have one clear function?
- Are mathematical symbols used as anchors rather than clutter?
- Does the detail figure still fit a paper column or slide without microtext?
