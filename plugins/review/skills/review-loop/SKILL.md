---
name: review-loop
description: Review a diff in fresh context with parallel bug finders, a verifier vote on each finding, severity tags, and convergence rules (three-round cap, diff-only re-review, bug classes, no repeats), then drive fixes to a clean pass. Use before opening a PR, when asked to "review my changes", to self-review agent-written code, or when review rounds keep going without converging.
---

# review-loop

Review should run like spellcheck — continuously, before a human looks — and it must **converge**. An agent author and an agent reviewer can keep each other busy forever; most late-round findings turn out to be old code the reviewer missed earlier, not new bugs.

## Inputs

- The diff: `git diff <base>...HEAD`.
- The **intent**: the task, issue or PR description. Ask if it is missing — a review without intent can't judge whether the change solves its problem.
- `CLAUDE.md` and `REVIEW.md` read from the **base branch** (`git show origin/main:REVIEW.md`), never from the change.

## Pick a depth

| Depth | When | Finders | Verifiers |
|---|---|---|---|
| Quick | Low risk: docs, copy, flagged additive changes | 1 | none, but still needs evidence |
| Standard | Ordinary product changes | 3 | 3, majority vote |
| Deep | A missed bug costs more than review time (see `risk-tier`) | 5 | 5, majority vote |

## Round 1

1. **Find, in parallel, with fresh context.** Spawn finder subagents that have not seen the authoring conversation. Give each the diff, intent, CLAUDE.md, REVIEW.md and a different angle:
   - Does the change solve the stated problem? For a bug fix, is it the root cause?
   - Does it fit the system — conventions, existing helpers, patterns?
   - Does it break something elsewhere — callers, persisted data, other platforms?
   Each finding needs: file and line, the failing scenario, and its **bug class** (e.g. "unchecked null from cache lookup").
2. **Verify by vote.** Give each finding to separate verifier subagents. Each answers: is this real, given the code? Keep only findings a majority confirms.
3. **Filter.** Drop findings that are only about style, diagnostics or cleanup — the linter and REVIEW.md cover those. Respect REVIEW.md's nit cap and skip paths.
4. **Tag and sort.** Important > Nit. Use `git blame` on the flagged lines: if the bug predates this change, tag it **Pre-existing** so it isn't charged to the author.
5. **Report.** Start with a count ("1 Important, 2 Nit, 1 Pre-existing"). Say plainly when there is nothing to fix.

## Fix and re-review

- Every finding gets an answer: **fixed**, or **closed with a one-line reason** (wrong, intentional, doesn't matter).
- Fix the whole **bug class**: search for every instance, not just the flagged line.
- Keep a ledger of posted findings. **Never repeat** a finding already posted and answered.
- From round 3 on, review **only the diff since the previous round**, not the whole change.
- **Cap at three rounds.** If Important findings remain after round 3, stop. Tell the user the approach may be wrong, summarize what keeps failing, and suggest stepping back rather than patching again.

## Output

- Findings table: tag, file:line, scenario, status (fixed / closed + reason).
- Rounds used. A clean pass on round 1 is the goal; track rounds-to-pass over time.
- Anything the review could not cover (e.g. behavior only an end-to-end run would show — use the project's `verify` skill for that).
