# claude-skills

Personal [Claude Code](https://code.claude.com) skills, packaged as a plugin marketplace.

## Install

```bash
/plugin marketplace add GeenccMustafa/claude-skills
/plugin install verification@claude-skills
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

## Principles

- **Verification means running the change.** End-to-end evidence beats passing unit tests.
- **Changes can't modify their own checks.** Gating rules are read from the default branch.
- **Failures are the signal for humans.** Three rounds, then escalate.
- **Misses become rules; rules get pruned.**

## Layout

```
.claude-plugin/marketplace.json
plugins/
  verification/
    .claude-plugin/plugin.json
    skills/<skill-name>/SKILL.md
```

## License

[MIT](LICENSE)
