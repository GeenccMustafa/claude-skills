---
name: structured-judgment
description: Evaluate candidates, vendors, tools, proposals or options with a structured procedure instead of a global impression — pick a few independent dimensions, score each one separately from factual evidence in a fixed order, combine with a simple formula, collect independent judgments before discussion, and only then consult intuition. Use for hiring and interview evaluation, vendor or library selection, choosing between designs, grading proposals, prioritizing a backlog, or any comparison where first impressions could dominate.
---

# structured-judgment

Global impressions are unreliable: one striking trait spreads a halo over everything else, and the order in which information arrives shapes the verdict. Simple, consistent rules that combine separately scored attributes usually match or beat holistic expert judgment in uncertain domains. Intuition is still useful — but only after the disciplined part is done.

## 1. Define the dimensions before looking at options

- Choose about 4–6 dimensions that matter for success and are as **independent** as possible (e.g. for a library: maintenance health, fit with our stack, performance on our workload, licence, security record, migration cost).
- For each dimension, write factual questions or measurable checks that inform it ("release in the last 3 months?", "p95 on our benchmark", "open critical CVEs"), and a 1–5 scale with what a 1, 3 and 5 look like.
- Decide the weights now. Equal weights are a strong default; don't tune weights after seeing results.

## 2. Score each dimension separately

- Gather evidence per dimension, then score **one dimension at a time across all options**, in a fixed order, before moving to the next.
- Write a one-line justification for each score, citing the evidence.
- Don't form or record an overall opinion until every dimension is scored.

## 3. Keep judges independent

If several people (or several subagents) evaluate:
- each scores alone first, without seeing others' scores,
- then compare, discuss only the large disagreements, and record the reason for any change.

Independent errors partly cancel out; correlated ones (everyone anchored by the first speaker) don't.

## 4. Combine with the formula

Compute the weighted score. Show the per-dimension table, not just the total.

## 5. Then consult intuition

Now form a holistic impression. If it disagrees with the formula, write down why. Override the formula only for a concrete, stated reason (a dealbreaker the dimensions missed) — not for a feeling. If you find a missed dimension, add it for every option, not just the one you prefer.

## For interviews

Ask the same factual, behavior-based questions of every candidate, score each trait right after its questions, keep notes of evidence rather than impressions, and decide only after all traits are scored.

## Output

```markdown
| Dimension (weight) | Option A | Option B | Option C |
|---|---|---|---|
| Maintenance (1) | 4 — release last month, 3 maintainers | 2 — last release 14 months ago | … |
| … | | | |
| **Weighted total** | | | |

**Intuitive check:** agrees / disagrees — why
**Recommendation:** … (and what would change it)
```
