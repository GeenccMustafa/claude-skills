# claude-skills

Personal [Claude Code](https://code.claude.com) skills, packaged as a plugin marketplace.

## Install

```bash
/plugin marketplace add GeenccMustafa/claude-skills
/plugin install verification@claude-skills
/plugin install review@claude-skills
/plugin install critical-thinking@claude-skills
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
| [`reliability-checklist`](plugins/verification/skills/reliability-checklist/SKILL.md) | Checks a diff against only the checklist items whose trigger matches, reading the checklist from the base branch. |
| [`misses-to-rules`](plugins/verification/skills/misses-to-rules/SKILL.md) | Turns recurring, diff-detectable misses into reviewed rules and prunes stale ones. |
| [`flaky-test-triage`](plugins/verification/skills/flaky-test-triage/SKILL.md) | Fixes flaky tests at the root cause — no sleeps, retries or skips; delete and document if unfixable. |
| [`pre-pr-check`](plugins/verification/skills/pre-pr-check/SKILL.md) | Runs cheap checks first, stops after three failed rounds, and stamps commits with `Verified-by:`. |

### `review`

Skills for reviewing code at the volume agents produce it, spending human attention where the risk is. Inspired by [How the Claude Code team does code review](https://claude.dev/blog/solving-code-review-at-anthropic/).

| Skill | What it does |
|---|---|
| [`review-md`](plugins/review/skills/review-md/SKILL.md) | Writes or tunes a short REVIEW.md (what failure looks like, nit cap, skip paths, evidence, output format) and checks the reviewer follows it. |
| [`review-loop`](plugins/review/skills/review-loop/SKILL.md) | Fresh-context parallel review with a verifier vote, Important/Nit/Pre-existing tags, and convergence rules: three-round cap, diff-only re-review, no repeats. |
| [`risk-tier`](plugins/review/skills/risk-tier/SKILL.md) | Classifies a change as low/medium/high from the change itself and says how many human approvals and how deep a review it needs. |
| [`pr-writeup`](plugins/review/skills/pr-writeup/SKILL.md) | Writes a PR description with evidence-backed Testing, Risk and How to revert sections for the requester to sign off. |
| [`reviewer-eval`](plugins/review/skills/reviewer-eval/SKILL.md) | Builds an eval from incidents, reverts and clean PRs; measures recall per stage, false positives, comment outcomes and rounds-to-pass. |
| [`review-gates-setup`](plugins/review/skills/review-gates-setup/SKILL.md) | Audits a GitHub repo's review layers (CI, AI and security review, CODEOWNERS, branch protection, merge queue, rollback) and proposes missing gates. |
| [`code-explainer`](plugins/review/skills/code-explainer/SKILL.md) | Explains one slice of the codebase as it is today, with file:line references and an optional diagram. |

### `critical-thinking`

Skills for deciding what is worth believing and acting on. The argument skills follow the critical questions in *Asking the Right Questions* by M. Neil Browne and Stuart M. Keeley; the judgment and decision skills draw on *Thinking, Fast and Slow* by Daniel Kahneman.

| Skill | What it does |
|---|---|
| [`argument-analysis`](plugins/critical-thinking/skills/argument-analysis/SKILL.md) | Full pass over an argument: issue, conclusion, reasons, ambiguity, assumptions, fallacies, evidence, rival causes, statistics, omissions and alternative conclusions. |
| [`assumption-finder`](plugins/critical-thinking/skills/assumption-finder/SKILL.md) | Surfaces hidden value and descriptive assumptions and ambiguous terms behind a plan or argument, and how to test the critical ones. |
| [`evidence-check`](plugins/critical-thinking/skills/evidence-check/SKILL.md) | Grades evidence by type (experience, examples, authority, surveys, research, analogies) and checks statistics for deception. |
| [`rival-causes`](plugins/critical-thinking/skills/rival-causes/SKILL.md) | Tests causal claims against rival explanations; useful for incidents, debugging and metric movements. |
| [`fallacy-check`](plugins/critical-thinking/skills/fallacy-check/SKILL.md) | Finds common reasoning fallacies, quotes them, and judges how much they matter to the conclusion. |
| [`self-critique`](plugins/critical-thinking/skills/self-critique/SKILL.md) | Strong-sense critique of your own position: steelman the other side, check thinking speed bumps, consider alternative conclusions. |
| [`bias-check`](plugins/critical-thinking/skills/bias-check/SKILL.md) | Audits a judgment or decision for predictable errors of fast thinking (anchoring, availability, base-rate neglect, halo, overconfidence, sunk cost…) and says when intuition can be trusted. |
| [`outside-view-estimate`](plugins/critical-thinking/skills/outside-view-estimate/SKILL.md) | Estimates from a reference class of similar past cases instead of the plan, and pulls intuitive predictions back toward the average. |
| [`premortem`](plugins/critical-thinking/skills/premortem/SKILL.md) | Assumes the plan has failed, collects independent failure stories, and turns the top ones into mitigations and tripwires. |
| [`structured-judgment`](plugins/critical-thinking/skills/structured-judgment/SKILL.md) | Compares candidates, vendors or options by scoring independent dimensions separately, combining them with a simple formula, and consulting intuition last. |
| [`choice-framing`](plugins/critical-thinking/skills/choice-framing/SKILL.md) | Checks risky choices for framing effects, loss aversion, sunk costs and rare-event distortion, and turns repeated decisions into a risk policy. |

## Principles

- **Verification means running the change.** End-to-end evidence beats passing unit tests.
- **Changes can't modify their own checks.** Gating rules are read from the default branch.
- **Failures are the signal for humans.** Three rounds, then escalate.
- **Misses become rules; rules get pruned.**
- **The change sets the risk tier, not the author.** Human attention goes where the risk is.
- **Review has to converge.** Cap rounds, re-review only new diffs, fix whole bug classes.
- **Pan for gold, don't soak like a sponge.** Question claims before accepting them, including your own.

## Sources

The skills are written in our own words, based on these sources:

| Source | Used for |
|---|---|
| Addy Osmani, [*How the Claude Code team thinks about verification*](https://x.com/addyosmani/status/2122590683055993308), X article, 17 Nov 2026 | `verification` plugin |
| Addy Osmani, Morgan Westlee Lunt and Qing Wang, [*How the Claude Code team does code review*](https://claude.dev/blog/solving-code-review-at-anthropic/), claude.dev blog, 15 Oct 2026 | `review` plugin, and the fresh-context review step in `pre-pr-check` |
| M. Neil Browne, Stuart M. Keeley and Mary Vasudeva, *Asking the Right Questions: A Guide to Critical Thinking*, 12th ed., Pearson, 2016 (ISBN 978-0-13-442563-4) | `critical-thinking`: `argument-analysis`, `assumption-finder`, `evidence-check`, `rival-causes`, `fallacy-check`, `self-critique` |
| Daniel Kahneman, *Thinking, Fast and Slow*, Farrar, Straus and Giroux, 2011 | `critical-thinking`: `bias-check`, `outside-view-estimate`, `premortem`, `structured-judgment`, `choice-framing`, and additions to `evidence-check`, `self-critique` and `argument-analysis` |
| [Hypothesis documentation](https://hypothesis.readthedocs.io/en/latest/) and the docs of the other libraries linked in the skill | `property-tests` skill |

## Layout

```
.claude-plugin/marketplace.json
plugins/
  verification/
    .claude-plugin/plugin.json
    skills/<skill-name>/SKILL.md
  review/
    .claude-plugin/plugin.json
    skills/<skill-name>/SKILL.md
  critical-thinking/
    .claude-plugin/plugin.json
    skills/<skill-name>/SKILL.md
```

## License

[MIT](LICENSE)
