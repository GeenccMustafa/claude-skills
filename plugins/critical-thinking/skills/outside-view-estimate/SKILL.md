---
name: outside-view-estimate
description: Make or check an estimate or forecast with the outside view — find a reference class of similar past cases, start from their actual outcomes, adjust only modestly for the specifics, and pull intuitive predictions back toward the average in proportion to how weak the evidence is. Use for project timelines, effort and cost estimates, roadmap commitments, launch or adoption forecasts, growth projections, and any prediction that feels confident because the plan looks good.
---

# outside-view-estimate

Plans are built from the inside view: the details of this project, as imagined by the people who will do it. That view reliably produces best-case estimates — the planning fallacy — because it ignores how often similar efforts ran into problems no one could list in advance. The outside view asks a different question: **how did cases like this one actually turn out?**

## 1. Get the inside-view estimate first

Write down the current estimate and its reasoning (the plan, task breakdown, assumptions). Don't argue with it yet; it is the starting point for adjustment.

## 2. Pick a reference class

Choose a set of past cases similar enough to compare: "features of this size in this codebase", "migrations of a service like this one", "integrations with a third-party API", "launches of a new paid tier". Too broad and it says little; too narrow and there are no data. If unsure, use two classes and compare.

## 3. Get the reference class statistics

Prefer real data over memory:
- the team's own history — issue tracker (estimate vs actual), `git log` between start and release tags, past project docs,
- published data for the category (industry studies, public postmortems),
- if nothing else, an explicit guess at the distribution, labeled as a guess.

Record the typical outcome **and** the spread: median overrun, how often it was 2× or worse, how often it was abandoned.

## 4. Baseline, then adjust

- Start from the reference-class outcome, not from the plan.
- Adjust **modestly** for specific reasons this case should differ (team has done this exact thing three times; dependency already exists). Write each reason down.
- Be suspicious of adjustments that all point in the optimistic direction.

## 5. Regress intuitive predictions

When the estimate is a number predicted from an impression (a candidate's future performance, a feature's expected uplift, a startup's growth):

1. Start from the average for the category (the baseline).
2. Note the number that matches your impression of the evidence (the intuitive prediction).
3. Estimate how well this kind of evidence actually predicts the outcome — from 0 (useless) to 1 (perfect).
4. Move from the baseline toward the intuitive number only by that fraction.

Weak evidence → stay near the average. Strong, proven predictors → move further. Do the same for ranges: the less predictive the evidence, the wider the range.

## 6. Present it

Give the outside-view estimate next to the inside-view one, with a range, not a point. If the gap is large, say what would have to be true for the inside view to be right, and consider a `premortem` before committing.

## Output

```markdown
**Inside view:** 6 weeks — plan: …
**Reference class:** last 8 features with a schema migration (issue tracker)
**Class outcomes:** median 1.7× planned; 3 of 8 took 2×+; 1 dropped
**Adjustments:** −10% (migration tooling now exists)
**Outside-view estimate:** ~9 weeks (range 7–13)
**What would make 6 weeks realistic:** …
```
