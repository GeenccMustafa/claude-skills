# claude-skills

Personal [Claude Code](https://code.claude.com) skills, packaged as a plugin marketplace.

## Install

```bash
/plugin marketplace add GeenccMustafa/claude-skills
/plugin install verification@claude-skills
/plugin install review@claude-skills
/plugin install critical-thinking@claude-skills
```

`team-review` is for teams with CODEOWNERS, several reviewers and an incident history. Install it only if that's you:

```bash
/plugin install team-review@claude-skills
```

Or from a local clone:

```bash
/plugin marketplace add ~/path/to/claude-skills
```

## Plugins

See [SKILLS.md](SKILLS.md) for a one-paragraph summary of every skill.

### `verification`

Skills that give Claude evidence-based feedback loops, so you review evidence instead of every diff. Inspired by [How the Claude Code team thinks about verification](https://x.com/addyosmani/status/2122590683055993308) by Addy Osmani.

| Skill | What it does |
|---|---|
| [`verify-setup`](plugins/verification/skills/verify-setup/SKILL.md) | Creates a project's own `verify` skill that boots, drives and inspects the real app (web, mobile, backend, CLI) and reports evidence. |
| [`property-tests`](plugins/verification/skills/property-tests/SKILL.md) | Finds round-trip, invariant, idempotency and equivalence properties and tests them with fast-check / Hypothesis / proptest. |
| [`differential-test`](plugins/verification/skills/differential-test/SKILL.md) | Runs old and new implementations on the same inputs, with normalization and an approved-differences list. |
| [`flaky-test-triage`](plugins/verification/skills/flaky-test-triage/SKILL.md) | Fixes flaky tests at the root cause — no sleeps or retries; quarantine with an issue, or delete and document, if unfixable. |
| [`pre-pr-check`](plugins/verification/skills/pre-pr-check/SKILL.md) | On request, runs cheap checks first, stops after three failed rounds, and stamps commits with `Verified-by:`. |
| [`reliability-checklist`](plugins/verification/skills/reliability-checklist/SKILL.md) | Checks a diff against only the checklist items whose trigger matches, reading the checklist from the base branch. |

### `review`

Small helpers that sit on top of the built-in `/code-review` rather than replacing it. Inspired by [How the Claude Code team does code review](https://claude.dev/blog/solving-code-review-at-anthropic/).

| Skill | What it does |
|---|---|
| [`review-md`](plugins/review/skills/review-md/SKILL.md) | Writes or tunes a short REVIEW.md (what failure looks like, nit cap, skip paths, evidence, output format) and checks the reviewer follows it. |
| [`pr-writeup`](plugins/review/skills/pr-writeup/SKILL.md) | Writes a PR description with evidence-backed Testing, Risk and How to revert sections for the requester to sign off. |

### `team-review`

Review governance for teams merging many agent-written PRs. These skills need inputs a solo repo usually doesn't have: CODEOWNERS, multiple human approvers, reverts and incidents.

| Skill | What it does |
|---|---|
| [`risk-tier`](plugins/team-review/skills/risk-tier/SKILL.md) | Classifies a change as low/medium/high from the change itself and says how many human approvals and how deep a review it needs. |
| [`review-gates-setup`](plugins/team-review/skills/review-gates-setup/SKILL.md) | Audits a GitHub repo's review layers (CI, AI and security review, CODEOWNERS, branch protection, merge queue, rollback) and proposes missing gates. |
| [`reviewer-eval`](plugins/team-review/skills/reviewer-eval/SKILL.md) | Builds an eval from incidents, reverts and clean PRs; measures recall per stage, false positives, comment outcomes and rounds-to-pass. |
| [`misses-to-rules`](plugins/team-review/skills/misses-to-rules/SKILL.md) | Turns recurring, diff-detectable misses into reviewed rules and prunes stale ones. |

### `critical-thinking`

Reasoning tools for engineering decisions: design docs, library choices, estimates, incidents. The argument questions follow *Asking the Right Questions* by M. Neil Browne and Stuart M. Keeley; the judgment and decision tools draw on *Thinking, Fast and Slow* by Daniel Kahneman.

| Skill | What it does |
|---|---|
| [`argument-analysis`](plugins/critical-thinking/skills/argument-analysis/SKILL.md) | Critiques an argument or your own position: conclusion, reasons, ambiguous terms, hidden assumptions, fallacies, evidence, statistics, omissions, alternative conclusions, and a steelman of the other side. |
| [`decision-check`](plugins/critical-thinking/skills/decision-check/SKILL.md) | Checks a judgment for predictable biases, scores options on independent dimensions before consulting intuition, and checks risky choices for framing and sunk costs. |
| [`rival-causes`](plugins/critical-thinking/skills/rival-causes/SKILL.md) | Tests causal claims against rival explanations; useful for incidents, debugging and metric movements. |
| [`outside-view-estimate`](plugins/critical-thinking/skills/outside-view-estimate/SKILL.md) | Estimates from a reference class of similar past cases instead of the plan, and pulls intuitive predictions back toward the average. |
| [`premortem`](plugins/critical-thinking/skills/premortem/SKILL.md) | Assumes the plan has failed, collects independent failure stories, and turns the top ones into mitigations and tripwires. |

## Principles

- **Verification means running the change.** End-to-end evidence beats passing unit tests.
- **Changes can't modify their own checks.** Gating rules are read from the default branch.
- **Failures are the signal for humans.** Three rounds, then escalate.
- **Don't rebuild what's built in.** Use `/code-review` and `/security-review`; add only what they lack.
- **Skills earn their place.** Narrow triggers, no overlap, and a skill that never fires gets removed.
- **Pan for gold, don't soak like a sponge.** Question claims before accepting them, including your own.

## Sources

The skills are written in our own words, based on these sources:

| Source | Used for |
|---|---|
| Addy Osmani, [*How the Claude Code team thinks about verification*](https://x.com/addyosmani/status/2122590683055993308), X article, 17 Nov 2026 | `verification` plugin, `misses-to-rules` |
| Addy Osmani, Morgan Westlee Lunt and Qing Wang, [*How the Claude Code team does code review*](https://claude.dev/blog/solving-code-review-at-anthropic/), claude.dev blog, 15 Oct 2026 | `review` and `team-review` plugins |
| M. Neil Browne, Stuart M. Keeley and Mary Vasudeva, *Asking the Right Questions: A Guide to Critical Thinking*, 12th ed., Pearson, 2016 (ISBN 978-0-13-442563-4) | `critical-thinking`: `argument-analysis`, `rival-causes` |
| Daniel Kahneman, *Thinking, Fast and Slow*, Farrar, Straus and Giroux, 2011 | `critical-thinking`: `decision-check`, `outside-view-estimate`, `premortem`, and additions to `argument-analysis` |
| [Hypothesis documentation](https://hypothesis.readthedocs.io/en/latest/) and the docs of the other libraries linked in the skill | `property-tests` skill |

## Layout

```
.claude-plugin/marketplace.json
plugins/
  verification/
  review/
  team-review/
  critical-thinking/
    .claude-plugin/plugin.json
    skills/<skill-name>/SKILL.md
```

## License

[MIT](LICENSE)
