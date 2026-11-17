---
name: choice-framing
description: Check a risky choice for framing effects — restate it as gains and as losses, compare options from a neutral reference point, ignore sunk costs, weigh rare events by their real probability, and evaluate it as one of many similar decisions under a consistent risk policy. Use for build-vs-buy, kill-or-continue, pricing, rollout, insurance-like and investment-style decisions, incident trade-offs, or whenever a choice is described as "avoid losing", "protect", "guaranteed" or "we've already invested".
---

# choice-framing

People don't evaluate outcomes in absolute terms; they evaluate changes from a reference point. Losses weigh roughly twice as much as equal gains, near-certainty and tiny probabilities get distorted weights, and the same facts in a different frame can flip a decision. Logically equivalent descriptions should lead to the same choice — this skill checks that they do.

## 1. State the options and the reference point

List the options with their likely outcomes and rough probabilities. Then name the implicit reference point: the status quo, the original plan, last quarter's number, a competitor, what was promised. Ask whether that reference point is actually the right one.

## 2. Reframe

Restate the choice in the opposite frame and see whether the preference survives:
- "keeps 90% of users" ↔ "loses 10% of users",
- "saves 2 of 6 services" ↔ "4 of 6 services still go down",
- "a 95% chance it works" ↔ "1 in 20 rollouts fails".
If the preferred option changes with the frame, the frame — not the facts — was deciding.

## 3. Check the usual distortions

| Distortion | Question |
|---|---|
| **Loss aversion** | Am I rejecting a good bet because the possible loss feels bigger than an equal gain? |
| **Status quo / endowment** | Would I choose the current option if I were starting fresh and owned neither? |
| **Sunk cost** | Does "we've already spent X" appear in the reasoning? Remove it; decide on future costs and benefits only. |
| **Certainty effect** | Am I overpaying to make a likely good outcome certain, or to eliminate a small risk completely? |
| **Possibility effect** | Is a vivid, unlikely outcome (huge win or catastrophe) getting more weight than its probability deserves? Write the actual probability next to it. |
| **Risk-seeking in losses** | Am I gambling to avoid accepting a sure loss (continuing a failing project hoping to recover)? |
| **Regret** | Am I choosing to avoid blame for acting rather than for the best expected result? |
| **Separate mental accounts** | Am I treating money or time differently depending on which budget it comes from? |

## 4. Think broad, not narrow

A single decision feels high-stakes on its own. Most organizations make many similar decisions (rollouts, experiments, vendor bets, hires). Ask:
- If we faced this kind of choice 20 times, which policy would we want to follow every time?
- Is a small favorable bet being rejected because it's viewed in isolation?

Write that as a **risk policy** ("we accept experiments with downside < X and positive expected value"; "we always canary to 5% first") and apply it consistently, instead of deciding each case by how it feels.

## 5. Decide

Recommend the option that holds up across frames, under a neutral reference point, without sunk costs, and consistent with the stated risk policy. Note any remaining reason that is genuinely about values (e.g. irreversibility, reputational harm) rather than a framing artifact.

## Output

```markdown
**Options:** …
**Reference point used / better one:** …
**Frame A → prefers:** … **Frame B → prefers:** …
**Distortions found:** …
**Broad-frame view / risk policy:** …
**Recommendation:** … — robust to framing? yes / no
```
