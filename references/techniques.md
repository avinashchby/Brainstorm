# Divergence Techniques — Reference

Six techniques for Phase 2. Apply all six to the reframed problem. No evaluation during this phase — generation only.

---

## 1. Direct

State the obvious approach. What would a competent engineer reach for first?

**Instruction:** Describe the most conventional solution without apology. One concrete paragraph.

**Example problem:** "Users forget to renew subscriptions."
**Direct output:** Build an email reminder sequence: 30 days before, 7 days before, 1 day before expiry. Standard drip campaign. Add a renewal button directly in the email.

---

## 2. Inversion

Solve the opposite problem, then invert the solution back.

**Instruction:** Ask "How would I make this problem as bad as possible?" Generate 2–3 sabotage moves. Then invert each into a real solution.

**Example:**
- Sabotage: "Remove all expiry notifications entirely."
  - Inverted: Surface expiry prominently everywhere — dashboard badge, email header, app banner.
- Sabotage: "Make renewal require 10 manual steps."
  - Inverted: One-click silent auto-renewal with opt-out, not opt-in.
- Sabotage: "Send reminders at times the user ignores email."
  - Inverted: Learn per-user preferred engagement time from open-rate history.

---

## 3. Constraint Removal

Identify the main constraint and ask what you would build if it didn't exist.

**Instruction:** Name the primary constraint explicitly. Then describe the ideal solution that only becomes possible once that constraint is lifted.

**Example:**
- Named constraint: "We can't store payment methods."
- Without it: Passive auto-renewal — no user action ever required. Colony detects stale subscription, charges saved card, sends receipt. Renewal rate approaches 100%.

Use this output to reverse-engineer: which part of the unconstrained solution can be approximated under the real constraint?

---

## 4. Constraint Addition

Restate the problem with a 10× resource reduction. What survives?

**Instruction:** Apply exactly one of these: 10× less time to build, 10× less code, 10× less budget, 10× fewer users to care about. State which one you chose. Design around it.

**Example (10× less code):**
- One cron job. Queries `WHERE expires_at < NOW() + INTERVAL 7 DAY`. Sends a single pre-written plain-text email. No personalization, no template engine, no analytics. Ships in an afternoon. Catches 80% of the problem with 5% of the effort.

Constraint addition forces elimination of accidental complexity.

---

## 5. Analogy Import

Find how a different domain solves the same underlying problem. Translate the mechanism.

**Instruction:** Name the domain. Name the mechanism. Map each element onto the current problem explicitly.

**Domains to consider (pick the best fit):**
- Aviation: pre-flight checklists, mandatory callouts, dual confirmation
- Medicine: triage, prophylactic treatment, symptom monitoring
- Urban planning: desire paths, traffic calming, signage placement
- Games: progressive onboarding, loss aversion, achievement unlocks
- Supply chain: just-in-time, safety stock, lead time buffers
- Finance: hedging, circuit breakers, margin calls

**Example (Games → Subscription renewal):**
- Mechanism: Loss aversion + countdown timer. Players act to avoid losing progress, not to gain rewards.
- Translation: Reframe renewal UI from "Renew to get benefits" → "Your data/progress deletes in 7 days unless you renew." Countdown clock. Progress bar emptying. Same information, opposite framing. Conversion lift without changing the product.

---

## 6. Devil's Advocate

Argue that every obvious approach will fail. Be specific. Name failure modes.

**Instruction:** Take the Direct solution and 1–2 others already generated. For each, write the concrete reason it fails in production. No vague "it might not scale" — name the specific failure scenario and when it occurs.

**Example:**
- Email reminders fail because: (a) deliverability drops below 60% for Gmail users after G-suite policy changes; (b) users who ignore 30-day notice ignore 7-day and 1-day notices — reminder fatigue is real; (c) the user who renews is often not the one who receives billing email (enterprise teams).
- One-click auto-renewal fails because: (a) card expiry creates silent failures with no retry logic; (b) GDPR Article 22 requires explicit consent for fully automated decisions involving payment in some jurisdictions; (c) chargebacks spike 40% when users feel surprised by charges.
- Inversion-derived solution fails because: (a) "deletion countdown" framing triggers fear → complaint tickets, not renewal. Works for games, backfires in B2B SaaS where users escalate to procurement.

Devil's Advocate output feeds directly into Phase 3 risk assessment and Phase 4 Risk scoring.
