---
name: reviewer-eval
description: Build and run an eval for an automated code reviewer from past incidents, reverts and known-clean PRs, and measure recall per stage, false positives, comment outcomes and rounds-to-pass. Use when tuning a reviewer's prompts, tools, model or REVIEW.md, when asked whether the AI reviewer is any good, or after an incident to add it as a test case.
---

# reviewer-eval

Review the reviewers. It is easy to catch more bugs by flagging everything, so every change to the reviewer is scored against real misses **and** against clean changes.

## 1. Build the case set

**Bug cases** — from reverts, fix-forwards and incident PRs:
- `gh pr list --state merged --search "revert in:title"`, `git log --grep -i "revert\|hotfix"`.
- For each, record: the PR that introduced the bug, the commit **before** it merged, and a **one-sentence answer key** naming the bug and its file/line.
- Have someone who knows that code confirm the answer key. Unconfirmed cases stay out.

**Clean cases** — merged PRs that stayed stable (no revert or fix within, say, 60 days), size-matched to the bug cases. They catch over-flagging.

Store cases in a versioned file, e.g. `evals/review/cases.yml`:

```yaml
- id: inc-2026-03-resume
  kind: bug
  repo_ref: 4f2c9a1          # base commit at review time
  pr_head: 9b7e002
  answer_key: "Loader throws on transcripts without `model` field (src/session/load.ts:88)"
- id: clean-1182
  kind: clean
  repo_ref: a13c0de
  pr_head: c55e91f
```

Split cases into a **tuning set** and a fixed **test set**. Tune only on the tuning set.

## 2. Run

For each case, recreate the repo at review time (`git worktree add <dir> <pr_head>`, base = `repo_ref`) and run the reviewer exactly as it runs on real PRs. Run cases in parallel where possible.

## 3. Score

- **Recall**: a bug case counts only if a finding describes the answer-key bug at the right place. Vague or wrong-location findings don't count.
- **Recall per stage**: raw findings → after verification vote → final posted review. A drop between stages means the pipeline is losing bugs it found.
- **False positives**: findings on clean cases that would have led someone to make a harmful change.
- **Severity**: did real bugs get tagged Important rather than Nit?
- **Rounds-to-pass** on recent real PRs (see `review-loop`).

## 4. Measure noise on live PRs

Pull review threads (`gh api repos/{owner}/{repo}/pulls/{n}/comments`) and classify how each comment was answered: **fixed**, **wrong**, **intentional**, **didn't matter**. A rising share of wrong/intentional means noise, and noise costs more when the author is an agent: it fixes the nit, which means another commit and another round.

## 5. Decide

- Priority, in order: catch real bugs, then cut review rounds.
- Keep a reviewer change only if test-set recall holds or rises without more false positives.
- Stop raising recall when the next gain would be overfitting the tuning set.
- Rescore whenever the reviewer's prompts, tools, model or REVIEW.md change; schedule it daily if the set is large.
- Every new incident becomes a new case.

## Output

A table per run: recall (raw / verified / final), false-positive rate on clean cases, severity accuracy, and the diff against the previous run, with the cases that flipped.
