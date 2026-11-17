---
name: pr-writeup
description: Write a pull request description with evidence-backed Testing, Risk and How to revert sections, keep the change small, and hand it to the person who asked for the change to sign off before posting. Use when opening or updating a PR, when the user asks for a PR description, or when a repo needs a PR template with these sections.
---

# pr-writeup

A reviewer should be able to judge a change from its evidence, not by re-deriving it from the diff. The person who asked for the change signs off on the write-up, even when Claude drafts it.

## 1. Check the size

Small changes are easy to review, debug and revert. If the diff mixes unrelated work or is very large (roughly 1,000+ changed lines outside generated files), propose a split before writing anything.

## 2. Gather evidence — don't claim what didn't run

- Commands that ran and their results (tests, lint, types, build) — from `pre-pr-check` if used.
- End-to-end evidence from the project's `verify` skill: screenshots, responses, logs.
- Review results from `review-loop`: counts and anything left open with a reason.
- Risk output from `risk-tier`.

If something wasn't run, say so in the write-up.

## 3. Write it

Use the repo's template (`.github/pull_request_template.md`) if it exists; make sure it has these sections, and offer to add them if not:

```markdown
## What and why
<the intent in 2–4 sentences; link the issue>

## Testing
- `npm test` — 412 passed
- E2E (verify skill): checkout flow ✅ (screenshot), refund flow ✅
- Not covered: Safari, because …

## Risk
Tier: Medium — touches src/cache/**, not behind a flag.
Blast radius: all users loading saved sessions.
What the checks would miss: behavior with sessions older than v2.

## How to revert
- `git revert <sha>` is safe; no data migration.
- Or turn off flag `new_cache` (no deploy needed).
```

Rules:
- **Testing** lists real commands and results, not "tested locally".
- **Risk** names the tier, the blast radius, and what the automated checks would *not* catch — that sentence tells a human where to look.
- **How to revert** must be concrete. If revert isn't safe (migrations, external side effects), say what is needed instead.

## 4. Sign-off

Show the draft to the user and ask them to confirm it before creating or editing the PR. Don't post it on your own.
