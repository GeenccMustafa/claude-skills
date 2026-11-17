# Skills

A short summary of every skill in this repo.

## verification

**verify-setup**
Creates a project's own `verify` skill: boots the real app (web, mobile, backend or CLI), drives the user flows a change touches, and reports pass/fail with evidence. Stress-tests the harness so it is fast and reliable.

**property-tests**
Finds properties that must always hold (round-trip, invariants, idempotency, equivalence) and tests them with thousands of generated inputs using fast-check, Hypothesis, proptest or similar.

**differential-test**
Runs the old and new implementation on the same inputs and flags every difference. Normalizes irrelevant noise and keeps a human-approved list of intended changes. Built for migrations, rewrites and upgrades.

**reliability-checklist**
Checks a diff against only the checklist items whose trigger matches it. Each item has a trigger, a check and the incident behind it. The checklist is read from the base branch so a change can't edit its own checks.

**misses-to-rules**
Turns recurring, diff-detectable misses (reverts, incidents, review comments) into rules for REVIEW.md, CLAUDE.md, the checklist, tests or hooks. Rules must survive attempts to disprove them and get human approval. Also prunes stale rules.

**flaky-test-triage**
Fixes flaky tests at the root cause, with no sleeps, retries or skips. If the cause can't be found, deletes the test and documents the lost coverage.

**pre-pr-check**
Runs the cheap checks first (format, lint, types, tests, build, then the end-to-end verify skill), stops after three failed rounds and asks a human, and stamps the commit with a `Verified-by:` trailer.
