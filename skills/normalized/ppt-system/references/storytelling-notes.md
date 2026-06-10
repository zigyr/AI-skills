# Storytelling Reference

## Purpose

A reference on narrative rhythm, cognitive load management, and effective presentation structure. These are **theoretical foundations** — they inform the orchestrator's Narrative Planning stage and the Narrative Policy.

---

## Core Narrative Rhythm

### Tension → Reveal → Validation → Resolution

The fundamental rhythm of an effective presentation follows a four-beat cycle:

| Beat | Function | Audience State |
|------|----------|---------------|
| **Tension** | Surface a problem, gap, or question | "What's going on here?" — curiosity or concern |
| **Reveal** | Present the key insight or discovery | "I didn't know that" — surprise or reframing |
| **Validation** | Provide evidence that the insight is real | "That checks out" — trust and credibility |
| **Propose** | Offer the resolution or next step | "Let's do that" — conviction and readiness |

This cycle can repeat at multiple scales:
- **Micro-cycle**: within a single section (3–5 slides)
- **Macro-cycle**: across the entire presentation (the full arc)

### Sequencing Example

```
[Macro] Tension: "Our industry is changing in ways we didn't predict"
  [Micro] Tension: "Customer behavior has shifted"
  [Micro] Reveal: "The data shows a 40% drop in traditional channels"
  [Micro] Validation: "Here's what the top 3 competitors are doing about it"
  [Micro] Propose: "We need to reallocate resources now"

[Macro] Reveal: "We've identified a new growth vector"
  [Micro] Tension: "The current product misses this segment entirely"
  [Micro] Reveal: "This underserved segment is growing 3x faster"
  ...

[Macro] Propose: "Here's the plan and what we need from you"
  ...
```

---

## Cognitive Momentum

### Principles

**Progressive narrowing of ambiguity.** Early slides can be broad and open-ended. Each subsequent slide reduces uncertainty. By the final slide, the audience should experience clarity and conviction — the opposite of confusion.

**Clarity increases over time.** The presentation should feel like it's gaining focus, not losing it. If the audience is more confused on slide 20 than slide 5, the momentum has reversed.

**Density and whitespace alternate.** Cognitive load is managed through rhythm — periods of high information intake followed by periods of integration (breathing pages, quotes, images).

### The Momentum Curve

```
Clarity
  ↑                              ████████
  │                          ████
  │                      ████
  │                  ████
  │              ████
  │          ████
  │      ████
  │  ████
  └──────────────────────────────────────→ Time

  Early: broad, exploratory, lower clarity (by design)
  Mid:   narrowing, evidence accumulating, clarity rising
  Late:  convergent, resolved, maximum clarity
```

### Momentum Killers

- **Backtracking**: returning to a topic the audience thought was resolved
- **Static repetition**: saying the same thing in different words without advancing
- **Premature detail**: diving into specifics before establishing why they matter
- **False resolution**: signaling a conclusion, then continuing with more content

---

## Audience Cognitive States

Understanding where the audience is mentally at each stage:

| Stage | Audience Question | What They Need |
|-------|------------------|----------------|
| Opening (first 2 min) | "Why should I listen?" | Hook, relevance, emotional anchor |
| Context (min 2–5) | "What's this about?" | Framework, scope, map of what's coming |
| Core (min 5–15) | "Is this true? Does it matter?" | Evidence, examples, data, logic |
| Shift (min 15–20) | "What does this mean for me?" | Implications, reframing, stakes |
| Close (last 2 min) | "What do I do now?" | Clear call to action, single takeaway |

---

## Information Architecture Patterns

### The Pyramid Principle (Barbara Minto)

Start with the conclusion, then support it with arguments, then support arguments with data.

```
        Conclusion
       /    |    \
  Argument Argument Argument
   /  \     /  \     /  \
Data Data Data Data Data Data
```

**Application to slides**: The slide title is the conclusion. The slide body provides the supporting arguments and data. Every slide can stand alone as a mini-pyramid.

### The Sparkline (Nancy Duarte)

Alternate between "what is" (current reality) and "what could be" (future possibility). The gap between them creates dramatic tension.

```
What could be ──╮          ╭──╮          ╭─────
                ╰──────────╯  ╰──────────╯
What is ──────╯  ╰────────╮  ╰────────╮
                           ╯           ╰──────
```

**Application to slides**: Pair Problem (what is) with Vision (what could be). The contrast drives emotional engagement.

### The Hero's Journey

```
Ordinary World → Call to Adventure → Refusal → Mentor → Crossing Threshold →
Trials → Approach → Ordeal → Reward → Road Back → Resurrection → Return with Elixir
```

**Application to slides**: Not literal — but the emotional structure (stasis → disruption → struggle → transformation → resolution) maps well to product launches and vision presentations.

---

## Slide-Level Storytelling

### The 3-Second Rule

A slide should communicate its core message within 3 seconds of appearing. If the audience needs longer to decode what they're looking at, the slide is too complex.

**Test**: Show the slide for 3 seconds, then look away. Can you state its message in one sentence? If not, simplify.

### The 1-Minute Rule

A slide should be explainable by the presenter in approximately 1 minute. If a slide requires 3+ minutes of verbal explanation, split it into multiple slides.

### Title as Message

Every slide title should be a **complete thought**, not a topic label.

| Topic Label (weak) | Message Title (strong) |
|-------------------|----------------------|
| "Q3 Revenue" | "Q3 revenue grew 22%, exceeding projections" |
| "Market Overview" | "The market is consolidating around three dominant players" |
| "Our Product" | "Our platform reduces onboarding time by 60%" |
| "Next Steps" | "We recommend launching beta in Q1 with $500K budget" |

---

## Implementation in ppt-system

The orchestrator applies these storytelling principles during **Stage 2: Narrative Planning**:

1. Determine the macro narrative arc (Problem → Insight → Evidence → Solution → Decision)
2. Apply the tension/reveal/validation/resolution cycle at section level
3. Ensure progressive clarity (momentum curve slopes upward)
4. Validate that every slide title is a message, not a topic
5. Check 3-second and 1-minute rules across the planned sequence
