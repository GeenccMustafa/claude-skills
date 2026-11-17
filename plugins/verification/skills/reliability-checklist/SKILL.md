---
name: reliability-checklist
description: Check a diff against a project's reliability checklist, running only the items whose trigger matches the diff, or create/extend that checklist. Use before committing or opening a PR, when reviewing a change, when the user mentions past incidents or "things that always break", or when asked to set up a reliability checklist.
---

# reliability-checklist

Nobody should have to memorize past outages. A reliability checklist stores each lesson as an item with a **trigger readable from a diff**, a **check**, and the **incident or PR** it came from. For any change, only the matching items run — usually a handful.

## Checklist format

Store it in the repo, e.g. `.claude/reliability-checklist.md` (or `docs/reliability-checklist.md`). Each item:

```markdown
### RC-012: Old saved sessions still load
- Trigger: diff changes session storage, persisted message types, or their (de)serializers
- Check: new fields are optional or defaulted on load; loading a transcript written before this change still works (add or run a fixture from the previous format)
- Source: incident 2025-03-02 / PR #482
```

Rules for items:
- The trigger must be decidable from the diff alone (paths, symbols, file types, kinds of change).
- The check must be concrete enough to pass or fail.
- Every item cites where it came from. No source, no item.

## Running the checklist on a change

1. Read the checklist from the **base/default branch**, not from the change under review — a change must not be able to edit the checks that judge it (`git show origin/main:.claude/reliability-checklist.md`).
2. Get the diff (`git diff <base>...HEAD`).
3. For each item, decide whether its trigger matches. List matched items with the diff hunk that triggered them.
4. Run each matched check. Collect evidence (test output, reasoning tied to specific lines).
5. Report:

```
Matched 4 of 39 items.
RC-012 Old saved sessions still load — FAIL
  Trigger: src/session/schema.ts adds required field `model`
  Why: older transcripts have no `model`; loader throws
  Fix: default `model` on load + fixture test
RC-003 ... — PASS (evidence: ...)
```

Tag each finding **Important**, **Nit**, or **Pre-existing** (a bug that existed before this change — don't hold the author responsible).

If no checklist exists, say so and offer to create one (below).

## Creating or extending the checklist

Sources for items: postmortems, reverted PRs, hotfixes, recurring review comments. For each candidate:
- Confirm it happened at least once in a real incident or PR, and name it.
- Phrase a diff-readable trigger and a concrete check.
- Prefer one sharp item over a vague broad one.

Propose new items as a change to the checklist file for a human to approve; don't silently add them. Use the `misses-to-rules` skill when the source is a set of missed bugs.

## Hygiene

The checklist only grows if you let it. Periodically flag items whose trigger hasn't matched in a long time or whose underlying code was removed, and propose pruning them.
