# Scoring Rubric — Reference

Four-dimension scoring for Phase 4 convergence. Score each idea on all four dimensions before ranking.

---

## Dimensions

### 1. Impact (1–5)
Does this move the needle on the actual goal?

| Score | Meaning |
|-------|---------|
| 5 | Directly solves the core problem. Effect is large and measurable. |
| 4 | Solves most of the problem. One meaningful gap remains. |
| 3 | Partially solves it. Requires additional ideas to complete. |
| 2 | Tangentially related. Improves things but doesn't address the root cause. |
| 1 | Solves a symptom, not the problem. Or only helps in edge cases. |

**Anchor question:** "If this is the only thing we ship, how much better is the outcome?"

---

### 2. Effort (1–5)
How much build/change work does this require? Lower effort = higher score.

| Score | Meaning |
|-------|---------|
| 5 | Ships in < 1 day. Fewer than ~50 lines of new code or config change only. |
| 4 | Ships in 1–3 days. One engineer, no cross-team coordination. |
| 3 | Ships in 1–2 weeks. Requires design decisions or minor infra changes. |
| 2 | Ships in 1–2 months. Multiple engineers, new dependencies, or migrations. |
| 1 | Multi-quarter effort. Architectural change, significant risk, or team-wide coordination. |

**Anchor question:** "What is the real unit of work — not the optimistic estimate?"

---

### 3. Novelty (1–5)
Does this create durable advantage or is it immediately copyable?

| Score | Meaning |
|-------|---------|
| 5 | Unique mechanism. Hard to replicate without the same data, codebase, or operational knowledge. |
| 4 | Non-obvious approach. Takes competitors 6–12 months to understand and copy. |
| 3 | Differentiated execution of a known pattern. Copyable in 3–6 months with effort. |
| 2 | Known best practice. Competitors likely already have or could ship in weeks. |
| 1 | Commodity. Off-the-shelf solution available today. No moat. |

**Anchor question:** "If a well-funded competitor saw this tomorrow, how long until they ship it?"

---

### 4. Risk (1–5) — Inverted
Low risk = high score. High risk = low score.

| Score | Meaning |
|-------|---------|
| 5 | Fully reversible. Can be rolled back in minutes. No user-facing impact if it fails. |
| 4 | Low blast radius. Failure affects a small subset of users or is easily contained. |
| 3 | Moderate risk. Failure is visible but recoverable within hours. |
| 2 | High risk. Failure has downstream effects (data, billing, trust). Recovery takes days. |
| 1 | Critical risk. Failure could cause data loss, security incident, or significant churn. |

**Anchor question:** "What is the worst-case failure scenario and how long does recovery take?"

---

## Composite Score

```
Score = Impact + Effort + Novelty + Risk
Max = 20
```

Do not weight dimensions unless the problem context explicitly calls for it (e.g., a security-critical system warrants doubling Risk weight; a time-constrained MVP warrants doubling Effort weight). State any weight changes explicitly.

---

## Tie-breaking

When two ideas score within 2 points of each other:
1. Prefer the higher-Effort-score idea (lower build cost wins ties).
2. If still tied, prefer the higher-Risk-score idea (reversibility wins over novelty).

---

## Score Table Format

Output scores in this table:

| Idea | Impact | Effort | Novelty | Risk | Total |
|------|--------|--------|---------|------|-------|
| Idea A | 4 | 3 | 2 | 4 | 13 |
| Idea B | 5 | 2 | 4 | 2 | 13 |
| Idea C | 3 | 5 | 3 | 5 | 16 |

Narrative justification (1–2 sentences) required for any score of 1 or 5 — extreme scores must be defensible.
