---
name: brainstorm
description: Structured ideation framework — diverge/converge with 6 techniques, 3 evaluator lenses, 4-dimension scoring, and a permanent decision brief. Use when deciding between approaches, stuck on design, or starting something new.
argument-hint: <problem or decision to explore>
---

# Skill: Brainstorm

## When to use this skill
Invoke when the user says: "brainstorm", "help me think through", "explore options for", "what are my options", "I need ideas for", "think through this with me", "how should I approach", "let's brainstorm", "generate ideas for", "what's the best way to", "I'm stuck on", or starts with a design question.

## When NOT to use this skill
- "explain how X works" → explanation, not ideation
- "fix this bug" → debugging
- "write the code for X" → implementation, spec is already clear
- "review this code" → reviewer skill
- "what does X mean" → lookup

---

## Execution

Read the reference files before starting:
- `~/.claude/skills/brainstorm/references/techniques.md`
- `~/.claude/skills/brainstorm/references/perspective-lenses.md`
- `~/.claude/skills/brainstorm/references/scoring-rubric.md`
- `~/.claude/skills/brainstorm/references/output-template.md`

Then execute all 5 phases in order. Do not skip phases. Do not collapse phases.

---

## Discovery Phase (runs before Phase 1 on every invocation)

**Goal:** Ensure the problem has enough signal to produce useful ideas. Word count is not the signal — completeness is.

Analyze the input against 5 dimensions. Mark each Present (✓) or Missing (?):

1. **Actor** — Is there a specific person, role, or system experiencing the problem?
2. **Current state** — Is there a description of what happens today (status quo or failure mode)?
3. **Success metric** — Is there a concrete outcome that would mean "solved"?
4. **Tried/ruled-out** — Is there any indication of what's already been attempted or excluded?
5. **Primary constraint** — Is there a limiting factor (time, budget, technical, organizational)?

**Rules:**
- If **3 or more** are Missing: ask the 3 highest-priority missing questions in a single message. Wait for response before proceeding to Phase 1.
- If **1–2** are Missing: state your assumptions explicitly, then proceed.
- If **0** are Missing: proceed immediately.

**Question bank — pick the highest-priority missing ones:**
- Missing actor → *"Who specifically experiences this problem — what is their role and what are they trying to do when they hit it?"*
- Missing current state → *"What happens today without a solution — what's the workaround or the failure mode people live with?"*
- Missing success metric → *"What does a successful outcome look like in concrete terms — what would you measure or observe?"*
- Missing tried/ruled-out → *"What approaches have you already tried or ruled out, and why?"*
- Missing constraint → *"What's the primary constraint — time to ship, budget, technical complexity, or organizational buy-in?"*

Format as a numbered list. Accept partial answers and proceed — don't loop more than once.

---

## Phase 1: Problem Framing

**Goal:** Understand the real problem before generating any solutions.

Extract from the user's input:
1. **Problem statement** — one sentence, active voice, names the gap between current state and desired state.
2. **Three hidden assumptions** — beliefs embedded in how the problem was stated that might not be true. State each as: "We are assuming that [X]."
3. **Three reframes** — restate the problem from three angles:
   - **User goal angle:** What does the user ultimately want to achieve? State the problem in terms of their goal, not the mechanism.
   - **System constraint angle:** What can the system not do today? State the problem as a missing capability.
   - **Underlying need angle:** Strip away the stated solution space entirely. What is the deeper need this problem is a symptom of?

Output: Print all three reframes. Ask the user: "Which reframe feels closest to the real problem, or should I use all three?" Wait for confirmation before proceeding to Phase 2.

If the user says "all" or "continue" or gives no preference, use all three reframes as input to Phase 2.

**Language rule for Phase 1:** No solution language. Do not write "we could", "one option is", "I suggest". Pure framing only.

---

## Phase 2: Divergent Generation

**Goal:** Generate the widest possible solution space. Volume and variety matter. Quality filtering is strictly forbidden in this phase.

Read `references/techniques.md`. Apply all six techniques to the reframed problem(s) from Phase 1.

For each technique, generate one concrete idea. The idea must be specific enough that an engineer could start implementing it tomorrow.

**Output format — repeat the language rule at the top of each technique block:**

```
### 1. Direct [GENERATE ONLY — no evaluation]
[concrete idea]

### 2. Inversion [GENERATE ONLY — no evaluation]
[sabotage moves] → [inverted solutions]

### 3. Constraint Removal [GENERATE ONLY — no evaluation]
[named constraint] → [unconstrained ideal] → [approximation under real constraint]

### 4. Constraint Addition [GENERATE ONLY — no evaluation]
[which 10x reduction chosen] → [surviving design]

### 5. Analogy Import [GENERATE ONLY — no evaluation]
[domain] → [mechanism] → [translation to current problem]

### 6. Devil's Advocate [ARGUE AGAINST ONLY — no recommendations]
[failure modes for top 2–3 ideas already generated]
```

**Language rule for Phase 2:** No evaluative language at any technique. Do not write "this is better", "this won't work", "the best approach", "particularly promising". Generate only. After completing all 6 techniques, do a self-check: "Did I use evaluative language in any technique above? If yes, remove it now before listing ideas."

Devil's Advocate is the single exception — it explicitly argues against, but only after all other ideas are generated and only to name failure modes, not rank ideas.

At the end of Phase 2, list all generated ideas as a numbered flat list. Ask the user: "Which 3–4 ideas should I take into Phase 3 for deeper evaluation? Or I can select the most distinct ones automatically."

If the user says "you pick" or "auto" or "continue", select the 3–4 most distinct ideas — prioritize ideas from different techniques and different parts of the solution space.

---

## Phase 3: Perspective Injection

**Goal:** Stress-test the selected ideas through three evaluator lenses before scoring.

Read `references/perspective-lenses.md`. Apply all three lenses to each selected idea.

Run lenses in order: Skeptic → User/Customer → Lazy Engineer.

For each idea × lens combination, output the specific findings as described in the lens reference. Do not blend lenses mid-analysis.

**Language rule for Phase 3:** Observation and description only. No numerical scores yet. No ranking. Record what each lens reveals — don't conclude from it yet.

---

## Phase 4: Convergence and Ranking

**Goal:** Score all evaluated ideas, select a winner, explain the choice.

Read `references/scoring-rubric.md`.

1. Score each idea on all four dimensions (Impact / Effort / Novelty / Risk).
2. Output the score table.
3. Apply tie-breaking rules if needed.
4. State the recommended option.
5. Explain why this option over the others in 2–3 sentences, referencing lens findings (not just scores).
6. State what has to be true for the recommendation to succeed (2 critical assumptions).
7. State the falsification criteria: what result in the first week would tell you to switch?

---

## Phase 5: Output — Decision Brief

**Goal:** Produce a permanent, actionable decision record.

Read `references/output-template.md`.

1. Determine today's date (use the `date +%Y-%m-%d` Bash command).
2. Generate a slug from the problem statement: lowercase, hyphens, max 5 words. Example: "subscription-renewal-reminder-strategy".
3. Create the output directory and write the brief:
   ```bash
   mkdir -p docs/decisions
   ```
   Then use the Write tool to write `docs/decisions/YYYY-MM-DD-<slug>.md`. If Write fails (permission error), print the brief to chat only.
4. If `~/.hive/scripts/save.sh` exists (check with Bash `test -f ~/.hive/scripts/save.sh`), save each rejected option to hive memory using this exact pattern to handle quotes/apostrophes safely:
   ```bash
   printf '%s' "IDEA NAME: one-line reason rejected" | bash ~/.hive/scripts/save.sh --type decision --content "$(cat)" --project "$(basename $(pwd))" --importance 5
   ```
   Run once per rejected option.
5. Print the decision brief inline in the chat so the user can read it without opening the file.
6. End with: "Decision brief written to `docs/decisions/YYYY-MM-DD-<slug>.md`." and a one-line next action the user can take right now.

---

## Error Handling

- If the user interrupts mid-phase with "skip to results" or "just give me the answer", collapse Phases 2–4 but still output the Phase 5 decision brief. Note which phases were compressed.
- If `docs/decisions/` cannot be created (permission error, wrong directory), print the brief to chat only and note: "Could not write to docs/decisions/ — brief is inline only."
- If a reference file cannot be read, proceed with internalized knowledge of the technique/lens/rubric. Do not abort.
