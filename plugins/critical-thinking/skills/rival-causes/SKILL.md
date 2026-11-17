---
name: rival-causes
description: Test a causal claim ("X caused Y", "this change improved Z", "the outage happened because…") by generating rival explanations and comparing them against the evidence — correlation vs causation, after-this-therefore-because-of-this, reverse causation, common causes and multiple causes. Use for incident and postmortem analysis, debugging hypotheses, A/B test or metric movements, "why did this happen" questions, and any argument that rests on a cause.
---

# rival-causes

Most events have more than one plausible explanation. The more plausible rivals you can find, the less confidence the first explanation deserves until the evidence separates them.

## When to use it

Whenever a claim says or implies a cause: *because, led to, resulted in, drove, thanks to, due to, since we launched…*. Typical cases:
- a metric moved after a release,
- an incident or bug is attributed to one change,
- a team practice is credited for better results,
- a study links two things.

## 1. State the claimed cause precisely

`Claimed: A caused B.` Write what B is exactly (which metric, which time window, which users) and when A happened.

## 2. Check the shape of the reasoning

- **Association, not causation**: A and B occur together. Could B cause A (**reverse direction**)? Could C cause both (**common cause**)? Could it be chance — how many things were compared before this one stood out?
- **"After this, therefore because of this"**: B followed A in time. What else changed in the same window? (Deploys, config, traffic mix, seasonality, holidays, marketing, upstream providers, data pipeline changes.)
- ***The* cause vs *a* cause**: complex outcomes usually have several contributing causes. Is one being presented as the whole story?
- **Individual events**: explaining one person's or one system's behavior is especially uncertain; look for several contributing factors.

## 3. Generate rivals

Brainstorm at least three alternative explanations. Methods:
- Keep asking "why?" like a stubborn five-year-old.
- Take other perspectives: the user, ops/on-call, finance, a competitor, a skeptical statistician.
- Check the boring causes first: measurement or logging changes, sampling, caching, clocks/timezones, bots, data delays.
- Consider regression to the mean: an extreme value tends to be followed by a less extreme one regardless of any intervention.

## 4. Compare the explanations

For each candidate, including the original, judge:
- Does it make logical sense?
- Is it consistent with what else is known?
- Has this kind of explanation predicted or explained similar events before?
- How many of the observed facts does it explain, and how varied are they?
- Does anything known contradict it?

Then design the cheapest test that would separate the top candidates: a control group, a rollback, a holdout, a timeline query, a log search, reproducing the bug with and without A.

## Output

```markdown
**Claimed cause:** A → B
**Reasoning pattern:** association / sequence / single event / …
| Explanation | Fits facts | Contradicted by | Plausibility | Test to discriminate |
|---|---|---|---|---|
**Conclusion:** how confident the original claim deserves to be, and what to check next.
```

When writing your own causal argument (a postmortem, a results write-up), show that the relationship exists, that it runs in the direction you claim, and that it explains the facts better than the rivals you list.
