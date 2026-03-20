# Brainstorm

Structured ideation framework — diverge/converge with 6 techniques, 3 evaluator lenses, 4-dimension scoring, and a permanent decision brief.

![License](https://img.shields.io/badge/license-MIT-blue) ![Agent Compatible](https://img.shields.io/badge/agents-Claude%20Code%20%7C%20Cursor%20%7C%20Codex%20%7C%20Gemini%20CLI%20%7C%20Copilot-green)

## What It Does

Most agents treat brainstorming as free-form idea listing — this skill enforces a rigorous 5-phase process that prevents the two most common failure modes: jumping to solutions before the problem is understood, and picking an option based on gut feel rather than evidence. It opens with a Discovery phase that checks for completeness across 5 problem dimensions, then runs Problem Framing, Divergent Generation (6 techniques), Perspective Injection (3 evaluator lenses), and Convergence scoring before producing a permanent decision brief written to `docs/decisions/`. The output is an actionable record with a winner, two critical assumptions, and a falsification criterion — not just a list of ideas.

## When to Use This

- You say "brainstorm", "help me think through", or "explore options for" anything
- You are stuck on a design decision and need to widen the solution space before narrowing
- You need to decide between approaches and want scoring on Impact, Effort, Novelty, and Risk
- You are starting something new and want structured ideation before writing a spec
- You say "what's the best way to", "how should I approach", or "think through this with me"
- You want a permanent record of why a decision was made and what alternatives were rejected

## Key Features

- **Discovery phase** validates problem completeness across 5 dimensions (actor, current state, success metric, tried/ruled-out, constraint) before generating a single idea
- **6 divergence techniques**: Direct, Inversion, Constraint Removal, Constraint Addition, Analogy Import, and Devil's Advocate — applied in sequence with strict no-evaluation rules
- **3 evaluator lenses**: Skeptic (assumption stress-test), User/Customer (behavioral friction), and Lazy Engineer (minimum viable version) applied to the top 3–4 selected ideas
- **4-dimension scoring rubric**: Impact, Effort (inverted), Novelty, and Risk (inverted) on a 1–5 scale with tie-breaking rules
- **Decision brief output** written to `docs/decisions/YYYY-MM-DD-<slug>.md` with recommendation, critical assumptions, and falsification criteria
- **Hive memory integration** saves rejected options to `~/.hive/scripts/save.sh` when present, so ideas rejected today become candidates for future problems
- **Error handling** for mid-session interrupts, permission errors, and missing reference files — no hard aborts

## Quick Start

### Install (copy to your agent's skills directory)

```bash
# Claude Code
cp -r ~/Claude\ Code\ Skills/Brainstorm ~/.claude/skills/

# Or symlink for auto-updates
ln -s ~/Claude\ Code\ Skills/Brainstorm ~/.claude/skills/Brainstorm
```

### For other agents
```bash
# Cursor
cp -r ~/Claude\ Code\ Skills/Brainstorm .cursor/skills/

# Codex CLI
cp -r ~/Claude\ Code\ Skills/Brainstorm .codex/skills/

# Gemini CLI
cp -r ~/Claude\ Code\ Skills/Brainstorm .gemini/skills/
```

## Usage Examples

```
Brainstorm how to reduce churn in a B2B SaaS product where users go inactive after 30 days.
```

```
Help me think through how to structure authentication in a multi-tenant API — I need to decide between JWT, session cookies, and API keys.
```

```
I'm stuck on the data model for a notification system. Users can subscribe to events across multiple workspaces. Explore options for me.
```

```
Brainstorm approaches for making our CI pipeline 50% faster. We're on GitHub Actions, builds currently take 18 minutes.
```

```
What's the best way to handle schema migrations in a zero-downtime deployment? We have Postgres with ~40M rows in the affected table.
```

## Skill Structure

```
Brainstorm/
├── SKILL.md                          (178 lines — core 5-phase execution instructions)
└── references/
    ├── techniques.md                 (92 lines — 6 divergence techniques with examples)
    ├── perspective-lenses.md         (67 lines — Skeptic, User, and Lazy Engineer personas)
    ├── scoring-rubric.md             (98 lines — 4-dimension scoring with tie-breaking rules)
    └── output-template.md            (119 lines — decision brief template with writing rules)
```

Total: 554 lines across 5 files.

## Part of Forge Skills

This skill is part of the [Forge Skills](../README.md) collection — 23 production-grade agent skills for modern development.

## License

MIT
