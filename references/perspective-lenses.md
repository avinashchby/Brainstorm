# Perspective Lenses — Reference

Three lenses for Phase 3. Apply all three to each of the top 3–4 ideas selected at the end of Phase 2.

Each lens is a distinct evaluator persona with a specific question set and decision threshold. Do not blend lenses — run each one in full before moving to the next.

---

## Lens 1: The Skeptic

**Persona:** A principal engineer who has seen 200 promising ideas die in production. Skeptical by default. Does not celebrate novelty. Respects evidence.

**Core question:** "What has to be true for this to work — and what's the probability each assumption holds?"

**Probes to apply:**
1. Name the single most load-bearing assumption. If it's wrong, the idea fails entirely. How confident are you that assumption holds? (0–100%)
2. What has been tried before that is similar? Why did it fail? Is this idea meaningfully different, or is it repeating history?
3. What is the minimum viable evidence that would convince a skeptic this works before full build? Can you get that evidence in < 1 week?
4. At 10× current scale, does this break? Where exactly?

**Output format:** For each idea, one paragraph: named assumption + confidence % + known prior failure + falsifiability criteria.

---

## Lens 2: The User/Customer

**Persona:** The actual human (or system) that receives the output of this solution. Not a product manager imagining a user — the concrete person or process at the end of the chain.

**Core question:** "Is this solving the problem I actually have, or the problem someone assumed I have?"

**Probes to apply:**
1. Who specifically is the user? Name a real category (e.g., "a solo founder checking Stripe at 11pm", not "our users"). What is their mental model when they encounter this solution?
2. What does the user have to do differently from what they do today? Every behavioral change is friction. Quantify the delta.
3. What is the user's first reaction when they encounter this for the first time, with no explanation? Is that reaction "oh good" or "what is this"?
4. If the solution works perfectly, what does the user tell a colleague about it? If they can't articulate it in one sentence, the value proposition is unclear.

**Output format:** For each idea, two sentences: user reaction on first encounter + what they'd tell a colleague.

---

## Lens 3: The Lazy Engineer

**Persona:** A senior engineer who will implement this. They are not lazy in a pejorative sense — they are allergic to unnecessary complexity. They will find every shortcut, every way to deliver 80% of the value with 20% of the work.

**Core question:** "What is the smallest possible version of this that still works? And what would I cut without anyone noticing?"

**Probes to apply:**
1. Which parts of this idea are load-bearing and which are decoration? Draw the line.
2. What existing tool, library, or service covers 70% of this without custom code?
3. If you had to build this in one day and deploy by EOD, what survives? What does that tell you about priority?
4. What maintenance burden does this create in 6 months? Is it proportional to the value delivered?

**Output format:** For each idea, a "Minimum Viable Version" description in 2–3 sentences + the one thing you'd cut first.

---

## Using the Lenses

Run each lens against each selected idea in sequence:

```
Idea A → Skeptic | User | Lazy Engineer
Idea B → Skeptic | User | Lazy Engineer
Idea C → Skeptic | User | Lazy Engineer
```

The output of all three lenses feeds directly into Phase 4 scoring. Do not score during Phase 3 — observe and note, do not evaluate numerically yet.
