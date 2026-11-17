---
name: fallacy-check
description: Scan reasoning for common fallacies — attacking the person, slippery slope, perfect-solution demands, appeals to popularity, questionable authority or emotion, straw person, false dilemma, explaining by naming, glittering generalities, red herrings, diversions and begging the question — and explain each one found in plain words. Use when reviewing debates, comments, proposals, marketing, political or opinion pieces, PR or design discussions, or your own draft argument.
---

# fallacy-check

A fallacy is a reasoning trick or mistake that makes a conclusion look better supported than it is. Many fallacies hide in a questionable assumption, so start there; others divert attention or quietly assume the conclusion.

## Approach

1. Lay out the conclusion and reasons (see `argument-analysis`).
2. For each reason, ask what must be assumed for it to support the conclusion. A false or doubtful assumption is often the fallacy.
3. Check whether the reasoning stays on the issue or drifts away from it.
4. Check whether any "reason" just restates the conclusion.

## Fallacies to check

| Fallacy | What happens | Example (tech) |
|---|---|---|
| **Attacking the person** | Rejects an idea by attacking whoever holds it | "Of course the frontend team wants a rewrite." |
| **Make-sense story taken as reality** | A plausible story is treated as if it were established fact | "Users probably churn because onboarding is long." (never checked) |
| **Slippery slope** | Claims one step will inevitably lead to extreme consequences, without support for each step | "If we allow one exception to the lint rule, the codebase will rot." |
| **Searching for a perfect solution** | Rejects a solution because it doesn't solve everything | "2FA doesn't stop all phishing, so why bother?" |
| **Appeal to popularity** | True or good because many believe or do it | "Everyone uses microservices now." |
| **Questionable authority** | Cites an authority without relevant expertise, or unnamed "experts" | "A famous founder says tests are a waste of time." |
| **Appeal to emotion** | Uses fear, pride, guilt or excitement instead of reasons | "Do you want to be the one who caused the next outage?" |
| **Straw person** | Distorts the opposing view into a weaker one, then attacks that | "So you want zero code review?" |
| **False dilemma** | Presents two options when more exist | "Either we rewrite it or we live with it forever." |
| **Explaining by naming** | Gives a label as if it were an explanation | "It failed because of technical debt." |
| **Glittering generalities** | Vague, positive words used to win approval without reasons | "This architecture is modern, clean and future-proof." |
| **Diversion / red herring** | Shifts attention to a different issue to escape the original one | Answering a security concern by talking about the launch date. |
| **Begging the question** | A reason assumes the conclusion it is supposed to prove | "This is the best framework because it's superior to the others." |

Also watch for fallacies covered elsewhere: confusing correlation with causation and after-this-therefore-because-of-this (`rival-causes`), faulty analogies and hasty generalization from small or biased samples (`evidence-check`).

## Rules

- Quote the exact sentence and name the fallacy; explain in one sentence why it weakens the argument.
- Don't over-label. A strong argument can contain one weak sentence; say how much the fallacy actually matters to the conclusion.
- A fallacy shows a reason is bad, not that the conclusion is false. Say what better reason could support it, if any.
- Apply the same check to arguments you agree with.

## Output

```markdown
| Quote | Fallacy | Why it's a problem | Impact on conclusion (high / low) |
|---|---|---|---|
```

End with: whether the conclusion still stands on the remaining, sound reasons.
