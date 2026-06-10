# Grammar → Skill Routing Table

## Purpose

This file defines the decoupled mapping from grammar types to execution skills. It is the single source of truth for which skill handles which grammar — neither grammars nor skills hold this knowledge directly.

## Routing Rules

Derived from the orchestrator's Skill Routing Rules:

| Capability Need | Routed Skill |
|----------------|-------------|
| Narrative structure & storytelling | `storytelling-skill` |
| Aesthetic judgment & visual refinement | `taste-skill` |
| HTML/SVG slide generation | `frontend-slides` |
| Spacing, hierarchy & layout polish | `frontend-polish` |

---

## Grammar → Skill Mapping

### Comparison Slide

| Capability | Skill |
|-----------|-------|
| Slide generation | `frontend-slides` |
| Aesthetic refinement | `taste-skill` |
| Layout polish | `frontend-polish` |

### Process Slide

| Capability | Skill |
|-----------|-------|
| Slide generation | `frontend-slides` |
| Narrative flow | `storytelling-skill` |
| Layout polish | `frontend-polish` |

### Metrics Slide

| Capability | Skill |
|-----------|-------|
| Slide generation | `frontend-slides` |
| Aesthetic refinement | `taste-skill` |
| Layout polish | `frontend-polish` |

### Quote / Emphasis Slide

| Capability | Skill |
|-----------|-------|
| Slide generation | `frontend-slides` |
| Typography & aesthetic refinement | `taste-skill` |
| Layout polish | `frontend-polish` |

### Framework / Model Slide

| Capability | Skill |
|-----------|-------|
| Slide generation | `frontend-slides` |
| Narrative structure | `storytelling-skill` |
| Aesthetic refinement | `taste-skill` |
| Layout polish | `frontend-polish` |

---

## Orchestrator Integration

The orchestrator follows this sequence when routing:

```
1. Assign grammar type to slide (e.g., "P3 = Comparison")
2. Query this routing table for the grammar → skill mapping
3. Apply global policy constraints (narrative / rhythm / visual)
4. Dispatch to skills in priority order:
   a. Generate (frontend-slides) — always first
   b. Refine (taste-skill) — aesthetic pass
   c. Polish (frontend-polish) — precision pass
   d. Narrate (storytelling-skill) — when narrative structure is needed
```

## Design Notes

- **Loose coupling**: skills know nothing about grammars; grammars know nothing about skills
- **Replaceability**: swap a skill by updating only this table (e.g., replace `taste-skill` with `impeccable` for a specific deck)
- **Priority**: skills are dispatched in generation → refinement → polish order; this table encodes the dependency chain
