---
name: review-gates-setup
description: Audit a GitHub repository's review pipeline layer by layer (CLAUDE.md and hooks, REVIEW.md, PR template, required CI, AI and security review, branch protection, CODEOWNERS, merge queue, flags and rollback) and propose the missing gates. Use when setting up a repo for agent-written PRs, when asked "how should we review at this volume", or when the user wants their repo's review process hardened.
---

# review-gates-setup

No single gate catches everything. Layer checks so few problems get through all of them, and make rollback fast for the rest. This skill **audits and proposes**; it changes repository settings only after the user approves each one.

## 1. Audit

Read, don't change:

```bash
gh repo view --json nameWithOwner,defaultBranchRef,mergeCommitAllowed,squashMergeAllowed
gh api repos/{owner}/{repo}/branches/{default}/protection        # may 404 = none
gh api repos/{owner}/{repo}/rulesets
ls .github/workflows .github/CODEOWNERS CODEOWNERS .github/pull_request_template.md CLAUDE.md REVIEW.md 2>/dev/null
```

Fill in this checklist with ✅ / ⚠️ / ❌ and a one-line note each:

**Before the PR**
- Short `CLAUDE.md` listing the commands that verify a change
- Hooks that run formatter and linter (see `.claude/settings.json`)
- A project `verify` skill (see `verify-setup`)
- Local review: `/code-review` and `/security-review`
- `REVIEW.md` (see `review-md`)

**On every PR**
- Required CI: lint, types, tests on every supported platform, build
- PR template with Testing, Risk, How to revert (see `pr-writeup`)
- AI reviewer on PRs (Code Review for Claude Code or the Claude Code GitHub Action)
- Automated security review (the security review GitHub Action)
- All review threads must be resolved before merge
- Review depth matched to risk; review rounds capped

**Approval**
- Written risk tiers, set from the change (see `risk-tier`)
- `CODEOWNERS` covering auth, billing, CI and release workflows, installers
- Branch protection: required status checks, required code owner review, dismiss stale approvals on new commits
- Bot approvals can't satisfy required human reviews

**Merge and after**
- Merge queue (checks re-run on the latest default branch)
- Feature flags, internal use first, staged releases
- One-step rollback; on-call or owner watching after merge
- Incidents and reverts feed a reviewer eval (see `reviewer-eval`)
- Human time per PR tracked, with revert/incident rate as the guardrail

## 2. Propose

Order fixes by value and effort. Start with one repo: add the AI reviewer, tune REVIEW.md for a few weeks, then widen. For each item give the exact change: a file to add, a workflow snippet, or the `gh api` call for a setting.

## 3. Apply — only with approval

- Files (templates, CODEOWNERS, REVIEW.md, workflows): make them on a branch and open a PR, if the user asks.
- Repository settings (branch protection, rulesets, merge queue): these change how everyone merges. Show the exact call and ask before running each one. Never loosen an existing protection without an explicit request.

## Output

The filled checklist, the top 3–5 proposed changes, and what was applied versus left for the user.
