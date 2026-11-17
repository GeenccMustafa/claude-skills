---
name: flaky-test-triage
description: Diagnose and fix flaky or intermittently failing tests at the root cause, without sleeps, retries or skips. Use when a test passes and fails on reruns, fails only in CI or only sometimes, depends on time, order or timing, or when the user says a test is flaky.
---

# flaky-test-triage

Flaky tests train agents to rerun instead of fix, and they hide real bugs. The rule: **find the root cause, or delete the test and write down why.** Never paper over it.

## Forbidden fixes

- Adding `sleep`/`wait(ms)`/arbitrary timeouts
- Wrapping in retries or marking it "retry until pass"
- `skip`/`xfail`/`.only`-ing it away without a decision
- Loosening the assertion until it can't fail

## 1. Reproduce

- Run the single test in a loop (e.g. 50–200 times) and record the failure rate.
- Run it in the full suite, in random order, and in parallel — many flakes only show up there.
- Try the CI conditions locally: same timezone, locale, CPU count, env vars, seed.
- Capture the full failure output each time.

If it never fails locally, compare environments and say so explicitly.

## 2. Classify the cause

Check the usual suspects:

| Cause | Signs | Real fix |
|---|---|---|
| Time / timezone / date | fails near midnight, month end, DST, in another TZ | inject a clock, freeze time, set TZ explicitly |
| Order dependence / shared state | passes alone, fails in suite | isolate state, reset fixtures, unique DB/schema per test |
| Async race | timing-sensitive asserts | await the real condition/event, not a delay |
| Randomness | different data each run | seed it, or make it a proper property test |
| External network/services | timeouts, rate limits | fake/mock at the boundary or run a local stub |
| Resource leaks / ports | "address in use", growing memory | close resources, dynamic ports |
| Floating point / unordered collections | tiny diffs, reordered output | tolerance, sort before compare |
| Real product bug | race in app code | fix the code, keep the test |

## 3. Fix and prove it

- Fix the root cause in the test **or** in the code — flakes are sometimes real concurrency bugs.
- Re-run the same loop from step 1. The fix is proven only if the failure rate drops to zero over a run count large enough to have caught the original rate.

## 4. If the root cause can't be found

Delete the test rather than keep a liar in the suite, and record:

- what behavior it was covering,
- what was tried and the observed failure rate,
- an issue or TODO to restore that coverage (by a better test, property test or E2E flow).

Put this in the commit message and, if the project tracks it, an issue — so the lost coverage stays visible.

## 5. Report

Failure rate before/after, root cause, fix, and any follow-up coverage that's now missing.
