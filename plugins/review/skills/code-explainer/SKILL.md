---
name: code-explainer
description: Write an explainer for exactly one slice of a codebase as it is today — purpose, entry points, data flow, key files, invariants and how to change it safely — optionally with a small diagram or visual page. Use when the user wants to understand a module, feature or flow before changing it, says "explain how X works", "walk me through", or is new to a part of the code.
---

# code-explainer

When machines do most of the line-by-line reading, people still need to understand the code they're about to change. An explainer for the exact slice you need teaches more than reading many small diffs, and it reflects the code as it is now.

## 1. Scope it

Ask (or infer from the request):
- **Which slice**: a module, a feature end to end, a request path, a data model.
- **Why**: about to change it, debugging, reviewing, onboarding. This decides what to emphasize.
- **How the person likes to learn**: prose, a diagram, a guided tour of files, examples. Default to short prose plus one diagram.

Keep the slice small. If it sprawls, propose splitting into two explainers.

## 2. Read the code, not the docs

- Find entry points (routes, commands, exported functions, UI screens) and follow the real calls.
- Read the tests — they show intended behavior and edge cases.
- `git log --oneline -15 -- <paths>` for recent changes and why they happened.
- Note where docs or comments disagree with the code; trust the code and say so.

## 3. Write the explainer

```markdown
# <Slice name>

**In one paragraph:** what it does and why it exists.

## Entry points
- `src/session/load.ts:42` `loadSession()` — called by …

## How data flows
<numbered steps from input to output, each with file:line>

## Key pieces
| File | Role |
|---|---|

## Invariants and gotchas
- <things that must stay true; surprising behavior; past incidents>

## Changing it safely
- Tests that cover it and how to run them
- What the reviewer/verify skill checks here
- Risky spots (see `risk-tier`)

## Recent changes
- <date> <sha> — <why>

## Open questions
- <what you couldn't confirm from the code>
```

Rules:
- Every claim about behavior points to a file and line.
- Mark guesses as guesses. List what you couldn't confirm.
- Prefer a diagram for flows with more than ~4 steps or several components (Mermaid in Markdown, or a small visual page if the environment supports publishing one).

## 4. Deliver

Give it to the user in the format they asked for. Offer to save it next to the code (e.g. `docs/explainers/<slice>.md`) only if they want it kept; explainers go stale, so regenerate rather than maintain them.
