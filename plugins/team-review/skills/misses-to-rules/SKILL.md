---
name: misses-to-rules
description: Turn bugs that slipped through — reverts, hotfixes, incidents, recurring human review comments — into rules for REVIEW.md, CLAUDE.md, the reliability checklist, or a hook, so the same miss doesn't happen twice. Also prunes stale rules. Use after an incident or revert, when the user says "this keeps happening", "make sure Claude never does X again", or asks to mine review comments or tidy up rules.
---

# misses-to-rules

A verification system improves by learning from what it missed. But rules that are vague, one-off or untested become noise. This skill only promotes a miss to a rule when it is real, recurring and detectable — and it keeps the rule set tidy.

## 1. Collect candidates

Pick the sources the user points to, or gather them:

- Reverted commits/PRs: `git log --grep -i revert`, `gh pr list --search "revert"`
- Hotfixes and incident/postmortem links
- Human review comments on merged PRs: `gh api repos/{owner}/{repo}/pulls/{n}/comments`
- Repeated test or check failures in the session or CI

For each, write down: what went wrong, the PR/commit, and the diff that introduced it.

## 2. Find patterns

Group candidates by the underlying mistake, not the surface symptom. A pattern qualifies as a **rule candidate** only if:

- it occurred in **at least two** separate PRs or incidents, **and**
- it is **identifiable from a diff** (a reviewer looking only at the change could spot it).

Single occurrences go into a "watch list" section in your report, not into rules.

## 3. Try to disprove each candidate

Before proposing a rule, argue against it — ideally with independent subagents, at least three passes:

- Would this rule have flagged the original bugs? Show it on each diff.
- Would it flag clean, merged-and-stable changes (false positives)? Check a few recent ones.
- Is it already covered by an existing rule, lint or type check?
- Is it phrased so a reviewer can apply it without extra context?

Drop or rewrite candidates that don't survive.

## 4. Choose where the rule lives

| Rule type | Home |
|---|---|
| Something a reviewer should look for | `REVIEW.md` |
| How Claude should behave while coding | `CLAUDE.md` |
| A trigger + check tied to an incident | reliability checklist (see `reliability-checklist`) |
| Must never happen, mechanically checkable | lint rule, test, or Claude Code hook |
| Mechanically checkable invariant in data/logic | property test (see `property-tests`) |

Prefer the most mechanical option that works: a test or hook beats prose.

## 5. Propose, don't impose

Write the rules as a single reviewable change (branch/PR or a diff shown to the user). Each rule cites its sources (PR/incident links) and the evidence from step 3. A human approves before it lands. Rules that gate changes must live on the default branch, where the change being judged can't edit them.

## 6. Prune

Rule files only grow if you let them. When asked to tidy up (or after adding rules), flag:

- rules that duplicate each other or an automated check,
- rules about code that no longer exists,
- rules that haven't fired or mattered in a long time,
- vague rules no one can apply.

Propose removals or merges with a one-line reason each.
