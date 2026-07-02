---
name: drawio-diagram-builder
description: Create, edit, replicate, and iteratively refine editable diagrams.net / draw.io figures in .drawio XML. Use when the user asks for a scientific figure, paper method diagram, ML/system architecture diagram, reference-figure reproduction, browser-verified draw.io output, or fixes for text overlap, arrows, colors, icons, fonts, and alignment in editable diagram form.
---

# Research Draw.io Diagram Builder

## Core Principle

Produce an editable `.drawio` diagram first. Prefer direct XML authoring and browser screenshot feedback over raster screenshots or opaque exports. The goal is a valid, editable, publication-style diagram that can be iteratively refined.

## When To Use

Use this skill when the user wants:

- An editable draw.io figure
- A paper method or architecture diagram
- Reference-image replication in draw.io
- Screenshot-driven diagram refinement
- Fixes for text overflow, arrows, spacing, icons, or alignment in a diagram

## Workflow

1. Gather the input type: prompt, paper, repo, screenshot, or mixed references.
2. Extract a visual spec: canvas size, regions, hierarchy, labels, colors, arrows, icons, and spacing.
3. If replicating a reference image, write a compact visual brief first:
   - coordinate inventory
   - layout grid
   - asset ledger
   - defect log
4. Author the `.drawio` XML with explicit `mxGeometry` positions and consistent styles.
5. Preview through draw.io locally or in-browser, then inspect a screenshot.
6. Fix concrete defects in small batches and repeat until the diagram is clean.

## Design Priorities

- Keep the diagram editable.
- Preserve exact technical labels when the user provides them.
- Use primitive shapes when object-level editability matters.
- Keep arrows semantically clear: flow, dependency, feedback, grouping, or fan-in/fan-out.
- Avoid embedding a screenshot as the final answer when a redraw is requested.

## Reference Inputs

Load reference material only when needed:

- `references/drawio-workflow.md` for the end-to-end process
- `references/xml-authoring.md` for XML shapes, styles, and text layout
- `references/reference-replication-protocol.md` for screenshot-based reproduction

## Output Contract

Return an editable `.drawio` file when the task is to draw, or a clear prompt/spec when the user is still in planning mode.

## Non-Negotiable Rule

Do not finalize from XML alone when the task is high fidelity. Compare against a rendered screenshot and fix visible defects before handing off.
