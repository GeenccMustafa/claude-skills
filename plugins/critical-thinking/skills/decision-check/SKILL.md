---
name: decision-check
description: Check a judgment or decision for predictable errors of fast thinking — anchoring, availability, base-rate neglect, small samples, halo, overconfidence, framing, loss aversion, sunk cost — and, when choosing between options, score them on independent dimensions before consulting intuition. Use for library, vendor or architecture choices, build-vs-buy, kill-or-continue, rollout trade-offs, hiring, prioritization, or when a conclusion feels obvious and was reached quickly.
---

# decision-check

Most judgment errors are not random. They are predictable failures of fast, intuitive thinking that slow thinking didn't catch. A strong feeling of confidence says the story is coherent, not that it is true, so check the judgment, not the feeling.

Pick the parts that fit:
- **A single judgment or recommendation** → steps 1–3.
- **Choosing between options** → add step 4.
- **A risky choice** (loss, sunk cost, rare events) → add step 5.

## 1. Write down the judgment

State the decision, the main reasons, the confidence, and how it was reached: quickly or deliberately, alone or in a group.

## 2. Check for common errors

Report only the rows that actually apply, with evidence.

| Error | Signs | Fix |
|---|---|---|
| **What you see is all there is** | A neat story from limited information | List what you'd need to know and don't. How does the conclusion change if those facts go the other way? |
| **Substitution** | A hard question ("will this scale?") answered with an easy one ("is it popular?") | Write the real question and check the answer addresses it. |
| **Anchoring** | The first number (the ask, last year's budget, the first estimate in a meeting) shaped the result | Make your own estimate before looking at the anchor. |
| **Availability** | Risk judged by how easily examples come to mind (the last outage, a viral post) | Look up actual frequencies. |
| **Affect / halo** | Liking the option colours its risks, benefits and every other trait | Assess dimensions separately (step 4). Be suspicious when an option wins on everything. |
| **Base-rate neglect** | A vivid description beats the statistics | Start from how often things in this category succeed (`outside-view-estimate`). |
| **Small samples** | Strong conclusions from one sprint, five users, one A/B day | Ask for the sample size before explaining an extreme result. |
| **Overconfidence** | Narrow ranges in an area where predictions are rarely checked | Widen ranges; ask how often similar confident calls turned out right. |
| **Hindsight / outcome bias** | Judging a past decision by its result | Judge it by what was knowable then and how it was made. |
| **Planning fallacy** | Best-case timelines with no look at similar past work | Use `outside-view-estimate` and run a `premortem`. |

**Should the intuition be trusted?** Only when the environment is regular **and** the person had long practice in it with quick, clear feedback. Debugging a familiar system often qualifies. Adoption, roadmap and market forecasts usually don't. Confidence alone never answers this, whether from experts or AI models.

## 3. Decide what to change

For each error found: how far could it move the conclusion, and what single action reduces it (get a base rate, collect independent estimates, reframe, enlarge the sample)? In groups, collect individual judgments **before** discussion so early speakers don't anchor everyone.

## 4. Comparing options: score, then consult intuition

1. **Define 4–6 independent dimensions before looking at the options** (for a library: maintenance health, stack fit, performance on our workload, licence, security record, migration cost). Give each a 1–5 scale with what 1, 3 and 5 look like, and factual checks ("release in the last 3 months?", "p95 on our benchmark", "open critical CVEs").
2. **Fix weights now.** Equal weights are a strong default. Don't tune them after seeing results.
3. **Score one dimension at a time across all options**, with a one-line justification citing evidence. Form no overall opinion until every dimension is scored.
4. **Keep judges independent.** Several people or subagents score alone first, then discuss only the large disagreements.
5. **Combine with the formula**, then form an intuitive view. Override the formula only for a concrete, stated reason, such as a dealbreaker the dimensions missed. If you find a missed dimension, score it for every option.

## 5. Risky choices: check the frame

- **Name the reference point** (status quo, the original plan, what was promised) and ask whether it's the right one.
- **Reframe**: "95% of rollouts work" ↔ "1 in 20 fails"; "keeps 90% of users" ↔ "loses 10%". If the preference flips, the frame was deciding, not the facts.
- **Sunk cost**: if "we've already invested X" appears in the reasoning, remove it and decide on future costs and benefits only.
- **Loss aversion / status quo**: would you choose the current option if you were starting fresh and owned neither?
- **Rare events**: write the actual probability next to any vivid catastrophe or jackpot. Don't overpay to remove a small risk entirely, and don't gamble to avoid accepting a sure loss.
- **Think broad**: if you faced this kind of choice 20 times, what policy would you follow every time? ("We always canary to 5% first." "We accept experiments with downside < X.") Apply it consistently.

## Output

```markdown
**Judgment:** … (confidence: …)
| Error | Evidence it's present | Direction of distortion | Fix |
|---|---|---|---|
**Trust in intuition here:** high / low — why

<!-- if comparing options -->
| Dimension (weight) | Option A | Option B |
|---|---|---|
| … | 4 — evidence | 2 — evidence |
| **Weighted total** | | |
**Intuitive check:** agrees / disagrees — why

<!-- if risky -->
**Frame A prefers / Frame B prefers:** … **Risk policy:** …

**Recommendation:** … — and what would change it
```
