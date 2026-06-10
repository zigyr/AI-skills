# Visual Consistency Policy

## Purpose

Define the global visual constraints that ensure **cross-slide consistency** in every presentation. These rules constrain typography, color, alignment, spacing, and chart styling — applied uniformly across all slides regardless of grammar type.

## Source

Directly derived from the orchestrator's **Visual Consistency Policy**.

> Consistency reduces cognitive load and improves readability.

---

## Typography Policy

### Font Family Limit

**Maximum 2 font families per deck.**

Recommended pairing patterns:
- **Display + Body**: 1 distinctive display font (titles, hero text) + 1 readable body font (labels, small text)
- **Mono + Sans**: 1 monospace (code, data) + 1 sans-serif (everything else)
- **Single family**: 1 font family with weight variation (light/regular/bold) for minimal decks

### Font Hierarchy

| Role | Size Range | Weight | Usage |
|------|-----------|--------|-------|
| Hero / KPI | 48–96px | Bold / Black | Quote/Emphasis slides, Metrics hero numbers |
| Slide Title | 28–42px | Bold / Semibold | Every slide's primary heading |
| Section Label | 18–24px | Medium / Regular | Supporting labels, axis titles |
| Body / Note | 12–16px | Regular / Light | Attribution, source lines, footnotes |

Hierarchy must be **consistent across slides** — if body text is 14px on slide 3, it must be 14px on slide 12.

### Font Rule Enforcement

- All slides in a deck share the same font hierarchy
- Weight contrast (bold vs regular) creates hierarchy — do not use size alone
- Minimum text size: 10px (anything smaller is illegible when projected)

---

## Color Policy

### Color Budget

**1–2 primary colors + neutral palette.**

| Role | Count | Description |
|------|-------|-------------|
| Primary | 1–2 | Brand color, accent, emphasis elements |
| Neutral | 3–5 | Backgrounds, text, borders, dividers |
| Semantic | 0–2 | Optional: red for negative, green for positive (used sparingly) |

### Color Usage Rules

- Backgrounds: consistent across all slides (same color or same gradient treatment)
- Text color: consistent (e.g., all body text is the same neutral shade)
- Primary color: reserved for emphasis — titles, key numbers, highlights, connectors
- Never use primary color for body text
- Semantic colors (red/green) only on Metrics or Comparison slides where they convey meaning

### Contrast Requirements

- Text on background: minimum 4.5:1 contrast ratio for body text, 3:1 for large text (≥24px)
- Text on image overlay: dark scrim or text shadow must ensure legibility

---

## Alignment & Grid Policy

### Grid System

All slides share a **strict grid system**:

- **Margins**: consistent on all four sides (e.g., 80px on 1920×1080 canvas)
- **Columns**: 12-column grid for complex layouts; 2–4 column for simple layouts
- **Gutter**: consistent spacing between columns

### Alignment Rules

- Every element must align to the grid — no free-floating elements
- Left-aligned text is the default; center-aligned only for Quote/Emphasis hero text
- Consistent vertical rhythm: elements snap to a baseline grid

---

## Spacing Policy

### Margin Consistency

Page margins are identical across all slides in a deck.

| Canvas Size | Recommended Margin |
|------------|-------------------|
| 1920×1080 (16:9) | 80–120px |
| 1024×768 (4:3) | 60–80px |

### Spacing Rhythm

Spacing follows a **limited scale** (e.g., 8px base unit):
- Small: 8–16px (within a component)
- Medium: 24–48px (between related components)
- Large: 64–96px (between sections, around hero text)

Only these three spacing tiers are used — no ad-hoc spacing values.

---

## Chart & Visualization Policy

### Unified Chart Styling

All charts and data visualizations across a deck share:
- **Color palette**: use the deck's primary + neutral colors, not chart defaults
- **Line weight**: consistent stroke widths
- **Font**: use the deck's body font for all chart labels and legends
- **Gridline style**: consistent across all charts (light, minimal, or none)

### Chart Simplification

- No 3D effects on charts
- No unnecessary gridlines
- Legends only when absolutely needed (prefer direct labeling)
- Remove chart borders / chartjunk

---

## Decorative Element Policy

### Boundaries on Decoration

- **Shadows**: allowed only for depth on overlay elements (cards on backgrounds). No heavy drop shadows.
- **Gradients**: allowed for backgrounds. Not for text or functional elements.
- **Borders / rules**: thin (1–2px), neutral color, used sparingly as dividers
- **Icons**: consistent style (all outlined or all filled, not mixed). Single source library per deck.
- **Rounded corners**: consistent radius across all cards/containers

### Prohibited

- Clip art or stock illustration styles inconsistent with the deck's aesthetic
- Decorative animations that don't convey information
- Mixed icon styles within a single deck

---

## Implementation

The orchestrator reads this policy during **Stage 5: Visual Refinement** and **Stage 6: Consistency Checking**:

1. Before visual generation: policy is passed to skills as constraints
2. After visual generation: each slide is checked against font, color, alignment, and spacing rules
3. Cross-slide audit: all charts verified for unified styling, all fonts verified for consistent sizing
4. Violations trigger re-generation of the offending slide
