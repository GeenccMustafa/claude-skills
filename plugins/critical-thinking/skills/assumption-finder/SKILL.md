---
name: assumption-finder
description: Surface the unstated value and descriptive assumptions, and the ambiguous key terms, that an argument, plan, spec or decision depends on, and judge which ones are questionable. Use when reviewing a proposal, design doc, roadmap, strategy or estimate, when the user asks "what are we taking for granted", "what could make this wrong", or when two people agree on facts but still disagree on the conclusion.
---

# assumption-finder

Assumptions are the invisible links between reasons and a conclusion. They are usually unstated, taken for granted, and they decide whether the argument holds. Find them before judging anything else.

## 1. Pin down the structure

Write the conclusion and the reasons in one line each. If they are unclear, run the first steps of `argument-analysis` first.

## 2. Clarify key terms

For each important abstract word (*simple, secure, fast, scalable, user-friendly, cheap, fair*):
- Write two reasonable but different meanings.
- Ask whether the argument works under both. If it only works under one, that reading is an assumption — state it.
- Ask whether a definition was chosen to make the conclusion easier to reach.

## 3. Find value assumptions

A value assumption is an unstated preference for one value over another *in this situation*. Disagreements that survive agreement on facts are usually value conflicts.

Typical conflicts in engineering and product decisions:

| Value A | vs | Value B |
|---|---|---|
| speed of delivery | | safety / quality |
| team autonomy | | consistency / standards |
| flexibility | | simplicity |
| short-term cost | | long-term maintainability |
| privacy | | personalization / insight |
| openness / transparency | | security |
| innovation | | stability |
| individual performance | | team collaboration |

Clues:
- **Consequences**: list the outcomes the author highlights and the ones they ignore. Caring about the first set over the second reveals the ranking.
- **Background**: what does someone in the author's role usually need to protect? Use this only as a clue — individuals differ from their group.
- **Reverse it**: if the opposite value were ranked first, would the conclusion change? Then it's a value assumption.

## 4. Find descriptive assumptions

A descriptive assumption is an unstated belief about how the world is, was or will be.

Ask, for each reason → conclusion link:
- "If this reason is true, what else must be true for the conclusion to follow?"
- "Supposing the reason is true, how could the conclusion still be false?"
- "What does this reason itself quietly depend on?"

Then play two roles:
- **The author**: if you had to defend this conclusion, what would you take for granted?
- **The opposition**: why would a reasonable person disagree? Their objection usually points at a hidden assumption.

Common descriptive assumptions in tech work:
- the past trend continues (traffic, adoption, prices),
- users behave the way the team does,
- the measured metric reflects the goal,
- a fix in one place doesn't shift the problem elsewhere,
- an approach that worked elsewhere works here (see the analogy checks in `evidence-check`),
- a dependency, vendor or API will stay available and unchanged,
- the estimate includes integration, migration and rollout work.

## 5. Judge them

For each assumption: **plausible / questionable / unknown**, with a one-line reason. Highlight the 1–3 assumptions that, if false, would most change the conclusion, and say how to test each one cheaply (a spike, a query, a user interview, a benchmark).

## Output

```markdown
| # | Assumption | Type (value / descriptive / definition) | Status | Why it matters | How to test |
|---|---|---|---|---|---|
```

Followed by: the critical assumptions in one paragraph.
