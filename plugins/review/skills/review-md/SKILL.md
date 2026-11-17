---
name: review-md
description: Write or tune a repo's REVIEW.md, the short file that tells an AI reviewer what matters in this code, and check that the reviewer actually follows it. Use when a repo has no REVIEW.md, when reviews are noisy or miss the point, when the same review comment keeps coming back, or when the user asks to set up or improve automated code review guidance.
---

# review-md

`CLAUDE.md` says what the project is. `REVIEW.md` says what a **bad change** looks like here. It is written by (or with) the code owners, it is short, and it is read from the default branch so a change can't rewrite the rules that judge it.

## 1. Gather inputs

- Existing `CLAUDE.md`, `REVIEW.md`, `CODEOWNERS`, contributing docs.
- Recent human review comments: `gh pr list --state merged --limit 30`, then `gh api repos/{owner}/{repo}/pulls/{n}/comments`. Group repeated comments — they are the first rules.
- Reverts and incident fixes (see `misses-to-rules` in the team-review plugin).
- Directory layout: which areas are critical, which are generated or vendored.

## 2. Write it — keep it short

Target well under a page per area. Use this skeleton:

```markdown
# REVIEW.md

## What failure looks like here
- src/billing/: charging the wrong amount or charging twice
- docs/: it lies — describes behavior the code doesn't have
- config/: it misroutes — traffic, flags or secrets go to the wrong place

## Focus on
- <3–7 concrete things owners always check, each tied to a past problem>

## Don't flag
- Style that the formatter/linter already enforces
- Generated, vendored and lock files: dist/, **/generated/**, *.lock

## Evidence
- Every finding cites file and line and explains the failing scenario.
- Don't infer behavior from a name; read the code it calls.

## Nits
- At most 3 nits per review. Skip them entirely on Important findings' PRs.

## Output
- Start with a count: "2 Important, 1 Nit, 0 Pre-existing."
- Tag each finding Important, Nit or Pre-existing (bug not introduced by this change).
- If there is nothing to fix, say so plainly in one line.
```

Rules for the content:
- Define failure **per area** in plain words; that steers the reviewer better than long checklists.
- Every "Focus on" item should come from a real recurring comment, revert or incident.
- In big repos, put a small `REVIEW.md` next to the code each team owns instead of one huge file.
- Keep `CLAUDE.md` short too: stack, conventions, goals, non-goals, the commands that verify a change. Link out to longer docs.

## 3. Check that the reviewer follows it

A REVIEW.md that the reviewer ignores is worse than none. Run the reviewer (e.g. `/code-review`) on 3–5 recent merged PRs and check:

- Did it respect the nit cap and the skip paths?
- Did every finding have file and line evidence?
- Did the summary start with a count, and say "nothing to fix" when clean?
- Did it catch the things in "Focus on" when they were present?

Rewrite any rule it doesn't follow until it does, or delete it.

## 4. Propose

Deliver REVIEW.md (and any CLAUDE.md trims) as one change for the code owners to approve. It only takes effect once it is on the default branch.

## Maintenance

When a review comment repeats across PRs, move it into REVIEW.md. When a rule stops mattering, delete it.
