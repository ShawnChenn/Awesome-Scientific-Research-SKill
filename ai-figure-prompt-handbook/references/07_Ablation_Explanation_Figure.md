# Ablation Explanation Figure

Use for explaining why components matter, showing contribution decomposition, or connecting ablation results to mechanism.

## Narrative Shape

Use cause and effect:

1. Full method.
2. Removed or varied components.
3. Mechanistic consequence.
4. Performance or qualitative effect.

## Prompt Skeleton

```text
Create an ablation explanation figure for [METHOD]. The figure should explain how each component contributes to [TARGET EFFECT].

Use a grid or layered comparison layout. Each row/card represents one component: [COMPONENTS]. Show the component, what changes when it is removed or altered, and the resulting effect. Use subtle metric badges or mini-bars only where they clarify the story.

Highlight the full method as the reference condition. Use muted styling for removed components and a clear accent for the key component. Keep labels short and avoid turning the figure into a dense numeric table.
```

## Design Checks

- Does the figure explain mechanism, not just report numbers?
- Are component removals visually unambiguous?
- Is the full method easy to compare against each ablation?
