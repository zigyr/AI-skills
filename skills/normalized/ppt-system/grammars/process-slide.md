# Process Slide Grammar

## Use Case

Present a sequence of steps, stages, phases, or actions that occur in order. The audience should understand the flow, the direction, and the relationship between steps.

Typical scenarios:
- Workflow or pipeline explanation
- Project phases / roadmap stages
- Decision flow or branching logic
- Methodology steps (3–7 steps)
- Timeline of events (variant: timeline layout)

## Narrative Role

- **explanation** — clarifies how something works or unfolds
- **progression** — shows advancement through stages
- **orientation** — helps the audience locate where they are in a process

## Layout Pattern

**Step flow layout** — sequential progression with clear directional cues.

Primary pattern: horizontal left-to-right flow with arrows or connectors.
Variant: vertical top-to-bottom for narrow or deep processes.
Variant: timeline (horizontal line with nodes) for time-based sequences.

Each step node contains:
- Step number or time marker
- Step name (short label)
- Minimal description (1 line max)

Connectors between nodes: arrows, chevrons, or timeline line segments.

## Information Density

**Low to Medium.** Each step must be digestible in isolation.

Maximum:
- 3–7 steps (5 is the sweet spot)
- 1 core action per step
- 1 supporting phrase per step (optional)

If a process exceeds 7 steps, group into phases (3–4 phases × 2–3 sub-steps each).

## Content Constraints

- Steps must be **sequential** — a clear before/after relationship exists
- Each step: **one verb-driven action** (e.g., "Collect data" not "Data collection process overview")
- Step labels must be **parallel in structure** (all noun phrases or all verb phrases, not mixed)
- Connector direction must be unambiguous
- Branching processes: limit to 2 branches at any decision point

## Cognitive Goal

Enable the audience to **mentally walk through the process** in a single pass. They should grasp both the sequence and the logic connecting steps.

## Visual Expectations

- Directional flow is immediately obvious
- Step nodes are visually equal in weight (unless emphasizing a specific stage)
- Connectors are clean and consistent
- Numbers or markers are prominent and sequential
- Progress feels natural, not forced

## Avoid

- Bidirectional or unclear flow direction
- Steps with mismatched granularity (mixing "Define strategy" with "Click the save button")
- Circular layouts unless the process genuinely loops
- Decorative arrows that don't aid comprehension
- Paragraph descriptions per step

## Recommended Skills

| Capability | Skill |
|-----------|-------|
| HTML/SVG slide generation | `frontend-slides` |
| Spacing & alignment polish | `frontend-polish` |
| Narrative flow design | `storytelling-skill` |
