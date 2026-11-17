---
name: pre-pr-check
description: Run the cheap local checks (format, lint, types, tests, build, then the project's verify skill) before committing or opening a pull request, fix what fails for up to three rounds, then escalate to a human, and stamp the commit with how it was verified. Use before any commit or PR, or when the user says "check before pushing", "make sure it's green", or "is this ready".
---

# pre-pr-check

Pushing an untested change spends shared review and CI time on bugs you could have caught yourself. Run the cheap checks first, locally, and leave a record of how the change was verified.

## 1. Discover the project's checks

Look in `package.json` scripts, `Makefile`, `justfile`, `pyproject.toml`, `Cargo.toml`, CI workflow files and `CLAUDE.md`. Build an ordered list, **cheapest first**:

1. format (check mode)
2. lint
3. type check
4. unit tests (affected first, then full if fast enough)
5. build
6. the project's `verify` skill (end-to-end), if it exists — see `verify-setup` if it doesn't

Use the exact commands CI uses where possible, so local green means CI green.

## 2. Run, fix, repeat — at most three rounds

For each failing check:
- Read the actual failure, fix the cause, and re-run that check.
- Don't weaken checks, add sleeps, skip tests or change config to make them pass. Flaky test? Use `flaky-test-triage`.
- Make sure the commit under test is the one you'll push: no edits after the last green run.

If the **same check still fails after three rounds**, stop. Summarize for the user what fails, what you tried, and your best hypothesis. Failures are the signal that a person needs to look.

## 3. Review the diff in fresh context

- If the repo has a reliability checklist, run the `reliability-checklist` skill on the diff and fix Important findings.
- Have a subagent that hasn't seen the authoring conversation review the diff against its intent (the `review-loop` skill in the review plugin, or `/code-review`). Fix Important findings, and stop at its three-round cap.

## 4. Stamp the commit

Add a trailer to the commit message recording how it was verified, so unverified commits are queryable later:

```
Verified-by: lint, types, unit, build, e2e
```

Use only what actually ran and passed. If nothing ran, write it honestly, with a reason:

```
Verified-by: none (docs-only change)
```

Query later with `git log --grep "Verified-by: none"`.

## 5. Report

A short table of each check, PASS/FAIL/SKIPPED (with reason), duration, and the evidence for the end-to-end run. Only then commit or open the PR — and only if the user asked for that.
