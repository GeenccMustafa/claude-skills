# Skills

A short summary of every skill in this repo.

## verification

**verify-setup**
Creates a project's own `verify` skill: boots the real app (web, mobile, backend or CLI), drives the user flows a change touches, and reports pass/fail with evidence. Stress-tests the harness so it is fast and reliable.

**property-tests**
Finds properties that must always hold (round-trip, invariants, idempotency, equivalence) and tests them with thousands of generated inputs using fast-check, Hypothesis, proptest or similar.

**differential-test**
Runs the old and new implementation on the same inputs and flags every difference. Normalizes irrelevant noise and keeps a human-approved list of intended changes. Built for migrations, rewrites and upgrades.

**flaky-test-triage**
Fixes flaky tests at the root cause, with no sleeps or retries. If the cause can't be found, quarantines the test with a tracked issue or deletes it, and documents the lost coverage.

**pre-pr-check**
When asked, runs the cheap checks first (format, lint, types, tests, build, then the end-to-end verify skill), stops after three failed rounds and asks a human, and stamps the commit with a `Verified-by:` trailer. Runs `/code-review` only for large or risky changes, or on request.

**reliability-checklist**
Checks a diff against only the checklist items whose trigger matches it. Each item has a trigger, a check and the incident behind it. The checklist is read from the base branch so a change can't edit its own checks.

## review

**review-md**
Writes or tunes a short REVIEW.md that tells the reviewer what failure looks like in each area, caps nits, lists paths to skip, requires file and line evidence, and asks for a summary that starts with a count. Then checks on recent PRs that `/code-review` actually follows it.

**pr-writeup**
Writes a PR description with evidence-backed Testing, Risk and How to revert sections, suggests splitting large changes, and hands the draft to the person who asked for the change to sign off.

## team-review

**risk-tier**
Classifies a change as low, medium or high risk from the change itself, not the author. Lists always-human paths (CI workflows, auth, billing, installers) and says how many human approvals and how deep a review the change needs.

**review-gates-setup**
Audits a GitHub repo's review pipeline layer by layer (instructions and hooks, CI, AI and security review, CODEOWNERS, branch protection, merge queue, flags and rollback) and proposes the missing gates. Changes settings only with approval.

**reviewer-eval**
Builds an eval for the AI reviewer from past incidents, reverts and known-clean PRs. Measures recall at each stage, false positives, how comments were answered and rounds-to-pass, and rescores whenever the reviewer changes.

**misses-to-rules**
Turns recurring, diff-detectable misses (reverts, incidents, review comments) into rules for REVIEW.md, CLAUDE.md, the checklist, tests or hooks. Rules must survive attempts to disprove them and get human approval. Also prunes stale rules.

## critical-thinking

**argument-analysis**
Critiques an argument, or your own position, with a fixed sequence of questions: issue and conclusion, reasons, ambiguous terms, value and descriptive assumptions, fallacies, evidence quality, deceptive statistics, omissions and alternative conclusions. For your own position it adds a steelman of the other side and a check for thinking speed bumps.

**decision-check**
Audits a judgment for predictable errors of fast thinking (anchoring, availability, base-rate neglect, small samples, halo, overconfidence, planning fallacy) and says when intuition can be trusted. For a choice between options, scores independent dimensions before consulting intuition. For a risky choice, checks framing, sunk costs, loss aversion and rare-event weighting, and turns repeated decisions into a risk policy.

**rival-causes**
Tests a causal claim by generating rival explanations (reverse direction, common cause, coincidence, other changes in the same window) and comparing them against the evidence. Useful for incidents, debugging and metric changes.

**outside-view-estimate**
Makes or checks an estimate by starting from how similar past cases actually turned out (the team's own history where possible), adjusting modestly for specifics, and pulling intuitive predictions toward the average when the evidence is weak. Counters the planning fallacy.

**premortem**
Assumes a nearly final plan has failed, gathers specific failure stories independently from several perspectives, and turns the top ones into mitigations, tripwires or a changed plan.

## cloud-governance

**governance-baseline**
Sets a cloud project's security and governance baseline at the start. Chooses IaaS, PaaS or SaaS per component by weighing control against who patches, then writes a one-page GOVERNANCE.md, IaC modules whose defaults are compliant, policy-as-code guardrails, ongoing compliance auditing and drift detection, automatic patching and edge DDoS protection. Tests each guardrail against a deliberately bad resource and changes live settings only with approval.
