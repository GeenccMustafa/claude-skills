---
name: argument-analysis
description: Critique an argument, or your own position, with a fixed sequence of critical questions — conclusion and reasons, ambiguous terms, hidden assumptions, fallacies, evidence quality, deceptive statistics, omissions and alternative conclusions. Use when asked to critique or "poke holes in" an RFC, design doc, proposal, vendor claim, benchmark, study or AI answer, or to steelman the other side of your own recommendation.
---

# argument-analysis

Read like a gold panner, not a sponge: keep asking questions and keep only what survives them. The aim is to decide what is worth believing and acting on, not to win.

Apply the same standard to arguments you like as to ones you dislike, including your own. Critical thinking used only against the other side is the weak kind.

## The questions, in order

Work through them in sequence. Write short answers that cite the text. Skip a step only when it clearly doesn't apply, and say so.

### 1. Issue and conclusion
- **Issue**: the question being answered. Descriptive ("what is true?") or prescriptive ("what should we do?")?
- **Conclusion**: the claim you are asked to accept. Look in the title, opening, closing, and after *therefore, so, this shows, we should*.
- No conclusion means nothing to evaluate yet. Say so.

### 2. Reasons
List each reason and lay out the structure: `Reason 1 → Reason 2 → Conclusion`. A conclusion without reasons is an opinion.

### 3. Ambiguous terms
For each key abstract word (*secure, scalable, simple, fast, fair, best practice*), write two reasonable readings. If the argument only works under one, that reading is an assumption. Ask whether a definition was chosen to make the conclusion easier.

### 4. Hidden assumptions
- **Value assumptions**: which value is ranked above another *here*? Common engineering conflicts: delivery speed vs quality, autonomy vs consistency, flexibility vs simplicity, short-term cost vs maintainability, innovation vs stability, privacy vs insight. Test: if the opposite value came first, would the conclusion change?
- **Descriptive assumptions**: for each reason → conclusion link, ask "if this reason is true, what else must be true for the conclusion to follow?" and "how could the conclusion still be false?" Typical ones in tech work:
  - the past trend continues (traffic, adoption, prices),
  - users behave like the team does,
  - the metric reflects the goal,
  - a fix here doesn't move the problem elsewhere,
  - what worked elsewhere works here,
  - the dependency, vendor or API stays available and unchanged,
  - the estimate includes integration, migration and rollout.

Rate each assumption **plausible / questionable / unknown**. Name the 1–3 that would most change the conclusion if false, and the cheapest way to test each (a spike, a query, a benchmark, a user interview).

### 5. Fallacies
Quote the sentence, name the fallacy, and say how much it matters. A fallacy shows a reason is bad, not that the conclusion is false. Don't over-label.

| Fallacy | Tech example |
|---|---|
| Attacking the person | "Of course the frontend team wants a rewrite." |
| Plausible story taken as fact | "Users probably churn because onboarding is long." (never checked) |
| Slippery slope | "One lint exception and the codebase will rot." |
| Perfect-solution demand | "2FA doesn't stop all phishing, so why bother?" |
| Appeal to popularity / authority | "Everyone uses microservices now." "A famous founder says tests are a waste." |
| Straw person | "So you want zero code review?" |
| False dilemma | "Either we rewrite it or live with it forever." |
| Explaining by naming | "It failed because of technical debt." |
| Glittering generalities | "Modern, clean and future-proof." |
| Red herring | Answering a security concern with the launch date. |
| Begging the question | "Best framework because it's superior to the others." |

### 6. Evidence
For each factual claim, name the evidence type and its main risk:

| Type | Ask |
|---|---|
| Intuition | Is the domain regular, and did this person get long practice with fast feedback in it? If not, it's a hypothesis. |
| Personal experience, anecdotes, testimonials | How were the cases picked? How many counter-cases exist? Any incentive? |
| Authority | Expert in *this*? Track record, not reputation? Do other experts agree? Who pays them? |
| Benchmarks, surveys, studies | Sample size and selection, exact measure or question wording, replication, who ran it, and whether it was run on a workload like yours. |
| Analogies | List the differences too. Do they matter to the conclusion? |

### 7. Statistics
- Could anyone actually know this number? How was it counted?
- Mean, median or percentile? A mean hides skew. Ask for p50/p95 for latency.
- Relative vs absolute change ("doubled" from 1 to 2), missing baseline or denominator, cherry-picked window, truncated axis, survivorship.
- Small samples produce extreme results by chance. Extreme results are usually followed by ordinary ones (regression to the mean).
- Does the number prove the conclusion, or something next to it? (More sign-ups ≠ more retained users. Fewer reported bugs ≠ fewer bugs.)
- For causal claims, use `rival-causes`.

### 8. What's missing
What would change your judgment if you knew it? The strongest counterargument, the real numbers behind *most, many, significantly*, costs and second-order effects, and who benefits if the conclusion is accepted.

### 9. Reasonable conclusions
Avoid either/or. Use if-clauses: "If the priority is cost, A; if it is reliability, B." Say which is best supported and how strongly.

## When the position is your own

Run the same questions, then:
- **Steelman** the other side as its best advocate would. If you can't make a convincing case against yourself, you don't understand the issue well enough yet.
- **Check the speed bumps**: Did I decide before gathering reasons? Am I trusting a source because I like something else about it (halo)? What evidence would change my mind, and did I look for it? Am I over-weighting the last outage or one loud user? Did I swap the hard question for an easier one? Would I reach this conclusion if I didn't want it to be true?
- **Rewrite for a critical reader**: conclusion first, reasons with sources, key terms defined, value priorities explicit, strongest counterargument acknowledged, confidence stated.

If the critique changes the conclusion, say so plainly.

## Output

```markdown
**Issue / Conclusion:** …
**Reasons:** 1) … 2) …
**Critical assumptions:** assumption — status — how to test
**Fallacies:** quote — name — impact (high / low)
**Evidence:** claim — type — strength (strong / moderate / weak / none)
**Statistics / missing information:** …
**Reasonable conclusions:** if …, then …
**Verdict:** accept / reject / hold — and what would change it
```

Name strengths as well as weaknesses. Prefer checking a primary source over trusting a summary, and say when you couldn't verify something.
