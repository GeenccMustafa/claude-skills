---
name: risk-tier
description: Classify a change's risk tier (low, medium, high) from the change itself, list the paths that always need a person, and say how many human approvals and how deep a review it needs. Use before requesting review or merging, when writing the Risk section of a PR, when deciding whether a change can merge on automated checks alone, or when setting up risk tiers for a repo.
---

# risk-tier

A docs fix and an auto-updater change shouldn't get the same review. **The change sets the tier, not the author.** Human attention goes where the risk is.

## Tier policy

Read the repo's policy from the default branch if it exists (e.g. `.claude/risk-tiers.md`). Otherwise use this default and offer to commit it:

| Tier | Examples | Human approvals | Review depth |
|---|---|---|---|
| Low | Docs, copy, tests only, internal-only features, additive changes behind a flag | 0 once CI, AI review and security review are green | Quick |
| Medium | Ordinary product changes; sensitive areas such as caching, updaters, system prompts | 1 | Standard |
| High | The highest-risk code and any always-two-people paths | 2 | Deep |

**Always-human paths** (at least one person, whatever the tier):
- anything listed as sensitive in `CODEOWNERS` or the policy file,
- CI and release workflows (`.github/workflows/**`, release scripts),
- auth, billing/payments, installers and auto-updaters,
- secrets handling and infrastructure config,
- anything irreversible: data migrations, deletions, public API removals.

Start strict. Loosen a tier only with evidence (revert and incident rates staying flat).

## Classify a change

1. Get the diff and touched paths: `git diff --stat <base>...HEAD`.
2. Match paths against always-human paths and the tier examples. The **highest** match wins.
3. Ask a second question even if the tier is low: *does this particular change need a person anyway?* Signals: hard to revert, not behind a flag, affects many users at once, touches persisted data formats, unclear intent, very large diff.
4. Apply the people rules:
   - Lighter paths only for authors on the repo's trusted list (usually the owning team). Others get one more human approval.
   - An agent's approval never counts as a human approval.
   - On an agent-written change, the person who directed the agent counts as one of the required reviewers.
   - An approval covers one commit. New commits the system can't vouch for (an agent push, a hand-resolved merge) need approval again.

## Output

```
Tier: Medium
Why: src/cache/** (sensitive area), not behind a flag
Always-human paths touched: none
Human approvals: 1 (the person who directed the agent counts; trusted author, so no extra approval)
Review depth: Standard
Suggestions: put behind a flag to drop to Low; split migration into its own PR
```

Keep the reasons concrete (paths and kinds of change). This output feeds the Risk section in `pr-writeup` and the depth in `review-loop`.
