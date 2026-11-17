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

## review

**review-md**
Writes or tunes a short REVIEW.md that tells the reviewer what failure looks like in each area, caps nits, lists paths to skip, requires file and line evidence, and asks for a summary that starts with a count. Then checks on recent PRs that the reviewer actually follows it.

**review-loop**
Reviews a diff in fresh context with parallel bug finders and a verifier vote on each finding, tags findings Important, Nit or Pre-existing, and drives fixes to a clean pass. Converges by design: three-round cap, diff-only re-review, fix whole bug classes, never repeat a finding.

**risk-tier**
Classifies a change as low, medium or high risk from the change itself, not the author. Lists always-human paths (CI workflows, auth, billing, installers) and says how many human approvals and how deep a review the change needs.

**pr-writeup**
Writes a PR description with evidence-backed Testing, Risk and How to revert sections, suggests splitting large changes, and hands the draft to the person who asked for the change to sign off.

**reviewer-eval**
Builds an eval for the AI reviewer from past incidents, reverts and known-clean PRs. Measures recall at each stage, false positives, how comments were answered and rounds-to-pass, and rescores whenever the reviewer changes.

**review-gates-setup**
Audits a GitHub repo's review pipeline layer by layer (instructions and hooks, CI, AI and security review, CODEOWNERS, branch protection, merge queue, flags and rollback) and proposes the missing gates. Changes settings only with approval.

**code-explainer**
Explains one slice of the codebase as it is today: purpose, entry points, data flow, key files with file:line references, invariants and how to change it safely, with an optional diagram.
