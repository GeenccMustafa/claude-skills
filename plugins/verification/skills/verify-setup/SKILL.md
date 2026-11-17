---
name: verify-setup
description: Create or improve a project's own `verify` skill — a fast, reliable smoke-test harness that boots the app, drives it like a user and inspects the result. Use when a repo has no `.claude/skills/verify/SKILL.md`, when the user asks to "set up verification", "make Claude test its changes end to end", or when an existing verify skill is slow, flaky or incomplete.
---

# verify-setup

Verification means **running the change**, not just running unit tests. Every project should carry its own `verify` skill that tells Claude exactly how to boot, drive and inspect the real system. This skill writes that project-specific skill.

## Outcome

A file at `.claude/skills/verify/SKILL.md` (or closer to the code it covers, e.g. `apps/web/.claude/skills/verify/SKILL.md` in a monorepo — add one per app if needed) that:

1. Boots the system in a known state.
2. Drives the user flows touched by a change.
3. Collects **evidence** (screenshots, HTTP responses, logs, exit codes).
4. Reports pass/fail per flow with that evidence.

## Steps

### 1. Detect what kind of system this is

Inspect manifests and entry points (`package.json`, `pyproject.toml`, `Cargo.toml`, `*.xcodeproj`, `build.gradle`, `Dockerfile`, `docker-compose.yml`, `Procfile`, existing CI config). Classify each runnable unit:

| Type | How Claude gets "hands and eyes" |
|---|---|
| Web app | Dev server + browser automation (built-in browser, Chrome extension, Playwright/CDP) |
| iOS / Android | Simulator/emulator MCP, build + launch + screenshot + tap |
| Desktop | Computer use, or the app's own test harness |
| Backend / API | Run locally, hit endpoints with `curl`/HTTP harness, read logs |
| CLI / library | Run the binary or a small driver script against real inputs |

### 2. Find the fastest reliable boot

- Prefer existing scripts (`dev`, `start`, `make run`) over inventing new ones.
- Identify required env vars, seed data, ports, and services (DB, queues). Use local/test values from the project's seed or example config — never real secrets.
- Measure the time to "ready". If it is slow, look for a faster path (skip unrelated services, use an in-memory DB, reuse a running server).

### 3. Build a feature map

List the user-visible features as flows, from the user's point of view:

```
- Flow: Sign in
  Path: /login → fill email + password → submit
  Selectors / endpoints: form#login, POST /api/session
  Expected: redirect to /dashboard, avatar visible
```

The feature map doubles as the grading rubric. Ask the user to confirm or add flows they care about most; do not guess business-critical flows silently.

### 4. Write the project's verify skill

Use this template:

```markdown
---
name: verify
description: Verify a change in <project> end to end before committing. Boots <system>, drives the affected flows and reports evidence. Use after changing user-visible behavior in <project>, before opening a PR, or when asked to check that it works.
---

# verify

## Boot
<exact commands, env, ports, readiness check, expected time>

## Pick flows
Map the diff to flows in the feature map below. Always run the smoke flow.

## Feature map
<flows from step 3>

## Drive and inspect
<per system type: how to navigate/call/tap, what to capture as evidence>

## Report
For each flow: PASS/FAIL, evidence (screenshot path, response, log excerpt), and for failures what is broken in one sentence.

## Rules
- Fix and re-run on failure. After 3 failed rounds on the same check, stop and ask a human, summarising what was tried.
- Never weaken a check, add sleeps, or retry until green to get a pass.
- Shut down anything you started.
```

### 5. Stress-test it

Run the new verify skill at least three times in a row, including once from a cold start. If any run is flaky or slow, fix the harness (readiness checks instead of sleeps, deterministic seed data, isolated ports) and repeat. The verify skill is the smoke-test harness: it must be rock solid before anyone relies on it.

### 6. Hand off

Tell the user where the skill lives, how long a typical run takes, which flows it covers and which it doesn't yet. Suggest adding "run the verify skill before committing" to the project's `CLAUDE.md`.
