---
name: bias-check
description: Audit a judgment, estimate or decision for predictable errors of fast, intuitive thinking — judging only from what's in front of you, answering an easier question, anchoring, availability, base-rate neglect, small samples, halo, overconfidence, hindsight and outcome bias, framing, loss aversion and sunk costs — and suggest the specific fix for each one found. Use before an important decision, when reviewing a recommendation, hiring or vendor choice, estimate, prioritization, postmortem, or whenever a conclusion feels obvious and was reached quickly.
---

# bias-check

The mind has two modes. A fast, automatic one produces impressions, stories and confident answers with no effort. A slow, deliberate one can check them, but it is lazy and usually just endorses what the fast one offers. Most judgment errors are not random; they are predictable failures of the fast mode that the slow mode didn't catch.

A strong feeling of confidence says the story is coherent, not that it is true. So check the judgment, not the feeling.

## 1. Write down the judgment

State the decision or judgment, the main reasons, and how confident you (or the author) are. Note how it was reached: quickly or after deliberate work, alone or in a group.

## 2. Check for common errors

Go through each row. Only report the ones that actually apply, with evidence.

| Error | Signs | Fix |
|---|---|---|
| **What you see is all there is** | A neat story from limited information; nobody asked what's missing | List what you would need to know and don't. Ask how the conclusion changes if the missing facts go the other way. |
| **Substitution** | A hard question ("will this hire succeed?") was answered with an easy one ("do I like them?") | Write the real question explicitly; check the answer addresses it. |
| **Anchoring** | A first number (the ask, last year's budget, the first estimate in a meeting) shaped the result | Generate your own estimate before looking at any anchor; argue against the anchor deliberately. |
| **Availability** | Judging frequency or risk by how easily examples come to mind (recent outage, vivid story, media) | Look up actual frequencies instead of recalled ones. |
| **Affect** | Liking or disliking the option drives the view of both its risks and benefits | Assess risks and benefits separately; be suspicious when an option looks good on every dimension. |
| **Base-rate neglect** | A vivid description beats the statistics ("this startup looks like a winner") | Start from the base rate for the category, then adjust (see `outside-view-estimate`). |
| **Plausibility over probability** | A detailed scenario feels more likely than a simpler one that contains it | Remember every added detail lowers probability; strip the story to its core claim. |
| **Small samples** | Strong conclusions from few data points (one sprint, five users, one A/B day) | Ask how big the sample is; small samples produce extreme results by chance. |
| **Regression to the mean ignored** | Praise/blame or interventions credited for a move back toward average | Expect extremes to be followed by less extreme results; compare against a control. |
| **Halo effect** | One strong trait (charisma, a famous logo, a great first demo) colours everything else | Evaluate dimensions separately (see `structured-judgment`). |
| **Overconfidence / illusion of validity** | Narrow ranges, high certainty, in an area where predictions are rarely checked | Widen ranges; ask how often similar confident predictions turned out right. Check whether intuition has earned trust here (below). |
| **Hindsight and outcome bias** | Judging a past decision by its result, "we should have known" | Judge the decision by what was knowable at the time and how it was made. |
| **Framing** | The same facts described as gain vs loss, survival vs mortality, would flip the choice | Restate in the opposite frame (see `choice-framing`). |
| **Loss aversion / status quo** | Rejecting a favourable change because giving something up looms larger | Compare options as if you didn't already own either. |
| **Sunk cost** | "We've already invested so much" is a reason to continue | Decide only on future costs and benefits from here. |
| **Planning fallacy** | Best-case timelines and budgets, no account of how similar projects went | Use the outside view (see `outside-view-estimate`) and run a `premortem`. |

## 3. Should this intuition be trusted?

Intuitive judgment is skilled only when **both** hold:
1. the environment is regular enough to be predictable, and
2. the person had long practice in it with quick, clear feedback on whether they were right.

Debugging a familiar system or reading a familiar codebase often qualifies. Long-range market, adoption, roadmap or stock forecasts usually don't. Confidence alone never answers this question — including the confidence of experts and of AI models.

## 4. Decide what to change

For each error found: how much could it move the conclusion, and what single action reduces it (get a base rate, collect independent estimates, reframe, run a premortem, enlarge the sample)? Group decisions: collect individual judgments independently **before** discussion so early speakers don't anchor everyone.

## Output

```markdown
**Judgment:** … (confidence: …)
| Error | Evidence it's present | Likely direction of distortion | Fix |
|---|---|---|---|
**Trust in intuition here:** high / low — why
**Revised judgment:** …
```
