# Decision Brief — Output Template

Use this template for Phase 5 output. Write to `docs/decisions/YYYY-MM-DD-<slug>.md` in the current working directory. Replace all `{{placeholders}}`.

---

```markdown
# Decision: {{one-line problem statement}}

**Date:** {{YYYY-MM-DD}}
**Status:** Proposed
**Decided by:** {{name or "pending"}}

---

## Problem

{{2–3 sentences. What is broken or missing? What is the measurable impact of not solving it?
No solution language here — only problem description.}}

## Hidden Assumptions Identified

1. {{Assumption 1 — what we assumed was true when framing this problem}}
2. {{Assumption 2}}
3. {{Assumption 3}}

## Reframes Considered

| Angle | Restatement |
|-------|------------|
| User goal | {{What the user actually wants to achieve}} |
| System constraint | {{What the system cannot do today, stated as a constraint}} |
| Underlying need | {{The deeper need beneath the stated problem}} |

---

## Options Evaluated

### Option 1: {{Name}} — Score {{total}}/20

**Source technique:** {{Direct / Inversion / Constraint removal / Constraint addition / Analogy / Devil's advocate}}

{{2–3 sentences describing the approach.}}

| Dimension | Score | Rationale |
|-----------|-------|-----------|
| Impact | {{1–5}} | {{one-line justification}} |
| Effort | {{1–5}} | {{one-line justification}} |
| Novelty | {{1–5}} | {{one-line justification}} |
| Risk | {{1–5}} | {{one-line justification}} |

**Skeptic finding:** {{key assumption + confidence %}}
**User reaction:** {{first encounter reaction}}
**Lazy engineer cut:** {{what gets cut first in MVV}}

---

### Option 2: {{Name}} — Score {{total}}/20

{{repeat structure above}}

---

### Option 3: {{Name}} — Score {{total}}/20

{{repeat structure above}}

---

### Rejected Options

{{List ideas generated but not in top 3. One line each: name + reason rejected.}}

1. {{Idea name}} — {{reason: too high effort / low impact / assumption fails / etc.}}
2. ...

---

## Recommendation

**Chosen:** {{Option name}}

**Why this over the alternatives:**
{{2–3 sentences. Reference scores and lens findings. Do not restate scores — explain the reasoning behind the choice.}}

**What has to be true for this to succeed:**
1. {{Critical assumption 1}}
2. {{Critical assumption 2}}

**Falsification criteria:** {{What result within the first week/sprint would tell you this is the wrong choice? State it concretely.}}

---

## Next Action

| Step | Owner | Due |
|------|-------|-----|
| {{First concrete action — specific enough to start tomorrow}} | {{name/role}} | {{date or sprint}} |
| {{Second action}} | {{name/role}} | {{date or sprint}} |

---

## Deferred

{{Ideas or sub-problems that surfaced during brainstorm but are out of scope for this decision.
Keep them — they are future decision seeds.}}

- {{Item}} — {{why deferred}}
```

---

## Writing Rules

1. The Problem section must not contain solution language. If you find yourself writing "we should" or "by doing X" in the Problem section, move it to Options.
2. The Recommendation must reference at least one lens finding. Scores alone do not justify a decision.
3. Next Actions must be specific enough that the owner can start without asking a clarifying question.
4. Rejected Options must be recorded. The hive memory integration saves these — ideas rejected today are candidates for future problems.
5. Status starts as "Proposed". Owner changes it to "Accepted" or "Rejected" after review. Never delete a rejected decision brief — rejection is information.
