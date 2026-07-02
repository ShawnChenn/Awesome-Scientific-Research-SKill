# Training Pipeline Figure

Use for training stages, data construction, pretraining/fine-tuning, inference pipelines, evaluation protocols, or agent workflows.

## Narrative Shape

Use process flow:

1. Data sources.
2. Transformation or sampling.
3. Model training or optimization.
4. Evaluation or deployment.
5. Feedback loop, if any.

## Reference Samples

When the user explicitly asks for a pipeline figure, read [Pipeline_Framework_Samples.md](Pipeline_Framework_Samples.md) for layout and structure cues.

## Prompt Skeleton

```text
Design a training pipeline figure for [METHOD]. Show the process from [DATA SOURCE] to [FINAL OUTPUT/EVALUATION].

Use a clean process diagram with [N] stages. Group data operations, model operations, and evaluation operations into visually distinct regions. Use arrows for temporal order and dashed arrows for optional feedback loops. Use small badges for losses, rewards, filters, or metrics.

Show these stages: [STAGES]. Highlight the important training signal: [LOSS/REWARD/OBJECTIVE].

Use a restrained palette with semantic colors for data, model, supervision, and evaluation. Avoid depicting the pipeline as a tangled graph; prioritize sequence and dependency clarity.
```

## Design Checks

- Can the reader follow the training order without reading the caption?
- Are data, model, and objective visually distinct?
- Are feedback loops clearly different from forward flow?
