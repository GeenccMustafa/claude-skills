---
name: premortem
description: Run a premortem on a plan or decision that is close to final — assume it has failed badly some time from now, generate the most plausible reasons it failed, independently and without debate, then turn the top reasons into mitigations, tripwires or a changed plan. Use before committing to a launch, migration, architecture choice, hire, investment, roadmap or any important decision, or when the user asks "what could go wrong".
---

# premortem

Once a group (or a single mind) is leaning toward a decision, doubts get suppressed: the story is coherent, the plan looks good, and raising concerns feels disloyal. A premortem makes doubt legitimate for a few minutes. Instead of asking "what might go wrong?", it states that the plan **did** fail and asks for the history of that failure — which unlocks reasons people were not voicing.

## When

The decision is nearly made but not yet committed. Earlier, there is no plan to attack; later, nobody will change it.

## 1. Set the scene

Write the decision in one paragraph: what will be done, by whom, by when, and what success looks like.

Then set the premise, with a concrete time horizon: *"It is <6 / 12> months from now. We went ahead with this plan, and the result was a clear failure. Write a short history of how it happened."*

## 2. Generate failure stories independently

- With people: everyone writes their reasons **alone and silently** for a few minutes before any discussion, so the first or most senior voice doesn't anchor the rest.
- With Claude alone: write failure stories from several distinct perspectives in separate passes — e.g. the engineer on call, the end user, the finance owner, a competitor, a security reviewer, the person who has to maintain it in two years. Use fresh subagents for each perspective if available.

Aim for concrete, specific failure stories, not generic risks ("the vendor raised API prices 4× after we migrated", not "vendor risk").

## 3. Cluster and rank

Group similar reasons. For each cluster estimate likelihood and impact, and note whether anyone could detect it early.

## 4. Act on the top reasons

For the top 3–5:
- **Mitigate**: change the plan to make it less likely or less harmful.
- **Tripwire**: define an early, observable signal and the action it triggers ("if p95 latency > 400 ms in the canary, roll back").
- **Accept**: explicitly, with an owner.
- **Reconsider**: if a reason threatens the whole decision, say so plainly.

## Limits

A premortem reduces overconfidence; it doesn't remove it, and it can't surface what nobody knows. Pair it with the outside view (`outside-view-estimate`) for timelines and budgets.

## Output

```markdown
**Decision:** …
**Premise:** It's <date>; it failed.
| Failure story | Likelihood | Impact | Early signal | Response (mitigate / tripwire / accept) |
|---|---|---|---|---|
**Plan changes:** …
**Does the decision still stand?** yes / yes with changes / reconsider — why
```
