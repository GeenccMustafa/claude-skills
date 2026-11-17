---
name: differential-test
description: Build a differential test harness that runs the old and new implementation on the same inputs and flags any difference — the old system is the oracle. Use for migrations, rewrites, framework or language ports, refactors, dependency upgrades, query/ORM changes, or any change where behavior is supposed to stay the same.
---

# differential-test

When behavior must not change, the old system is the best spec you have — better than docs that have drifted from production. Run both versions with the same inputs; every difference is either a bug or an approved change.

## 1. Define the two sides

- **Old**: the current production behavior — a git ref, a deployed build, the previous library version, the legacy service.
- **New**: the change under test.

Prefer running both in-process (import both modules) when possible; otherwise run them side by side as processes/services on separate ports. Pin the old side to an exact commit or version.

## 2. Choose inputs

In order of preference:

1. **Sampled real traffic** — recorded requests, logs, production-like datasets (scrubbed of personal data).
2. **Randomly generated inputs** — reuse property-test generators (see the `property-tests` skill).
3. **Existing test fixtures** — as a supplement, never the only source.

Aim for coverage of the input space, not just volume.

## 3. Normalize irrelevant differences

Write a `normalize()` step applied to both outputs before comparing:

- whitespace, key order, trailing newlines
- timestamps, generated IDs, random values
- float precision (compare with tolerance)
- ordering of unordered collections

Keep normalization minimal and explicit — every rule is a place a real bug could hide.

## 4. Keep an approved-differences list

Some differences are intended. Record them in a versioned file (e.g. `difftest/approved.yml`):

```yaml
- id: price-rounding-bankers
  match: "field: total, old rounds half-up, new rounds half-even"
  reason: "Product decision in PR #123"
  approved_by: "<owner>"
```

A difference is either on this list or it fails the run. Never add entries to make a run pass without a human-confirmed reason.

## 5. Run and report

- Run the harness, collect mismatches, and group them by shape (same field, same error class).
- For each group show: count, one minimal input, old output, new output, normalized diff.
- Fix bugs in the new side; propose approved-list entries only for clearly intentional changes and ask the user to confirm them.

## 6. Make it repeatable

Commit the harness, the normalization rules and the approved list next to the code so the comparison can run again on every change until the migration is complete. Remove it once the old side is gone.
