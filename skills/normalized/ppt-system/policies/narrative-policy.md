# Narrative Policy

## Purpose

Define the global narrative constraints that govern every presentation produced by the ppt-system. These rules apply **across all slides** — they shape the story arc, not individual page content.

## Source

Directly derived from the orchestrator's **Narrative Flow Rules** and **Presentation Philosophy**.

---

## Core Narrative Flow Rules

### 1. Progressive Storytelling

The presentation must advance. Each slide must either:
- Introduce new information, or
- Deepen understanding of previously introduced information

**Prohibited**: static repetition — re-stating the same point across multiple slides without adding depth or evidence.

### 2. Slide Type Alternation

Consecutive slides should not share the same grammar type. Rationale: cognitive variation maintains attention. A sequence of three Metrics slides in a row causes fatigue.

**Rule**: maximum 2 consecutive slides of the same grammar type before a different type must intervene.

### 3. Natural Transitions

Each slide must logically lead to the next. The transition can be:
- **Causal** (X causes Y)
- **Elaborative** (X explained → X evidenced)
- **Contrastive** (X vs Y)
- **Hierarchical** (Big picture → detail)

**Prohibited**: non-sequitur jumps where the connection between slides is unclear to the audience.

---

## Recommended Narrative Arc

```
Problem → Insight → Evidence → Solution → Decision
```

### Stage Definitions

| Stage | Function | Typical Grammar |
|-------|----------|----------------|
| **Problem** | Define the gap, tension, or challenge | Quote/Emphasis (hook), Framework (context) |
| **Insight** | Reveal the key understanding or discovery | Framework/Model, Quote/Emphasis |
| **Evidence** | Provide quantitative and qualitative support | Metrics, Comparison, Process |
| **Solution** | Present the resolution or recommendation | Process, Framework/Model, Comparison |
| **Decision** | Call to action or consolidated takeaway | Quote/Emphasis (closing), Metrics (impact) |

### Arc Variations

The narrative arc can be adjusted for different presentation types:

- **Pitch deck**: Problem → Solution → Evidence (traction) → Decision (ask)
- **Strategy report**: Context → Analysis (Evidence) → Insight → Recommendation (Solution)
- **Keynote**: Hook (Emphasis) → Vision (Insight) → Journey (Process) → Future (Decision)
- **Academic**: Question → Method (Process) → Findings (Metrics) → Implications (Insight)

---

## Audience Adaptation

Narrative strategy must account for audience:

| Audience | Evidence Density | Language | Pace |
|----------|-----------------|----------|------|
| Executive | Low — lead with conclusions | Direct, no jargon | Fast |
| Technical | High — lead with method | Precise, terms OK | Measured |
| Investor | Medium — lead with traction | Aspirational + data | Engaging |
| General | Low — lead with story | Accessible | Conversational |

---

## Implementation

The orchestrator reads this policy during **Stage 2: Narrative Planning** and applies it:
1. Determine the narrative arc structure based on presentation type
2. Plan the slide sequence following progressive storytelling
3. Ensure grammar type alternation across the sequence
4. Validate natural transitions between every adjacent slide pair
