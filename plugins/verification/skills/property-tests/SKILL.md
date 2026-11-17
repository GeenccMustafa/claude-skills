---
name: property-tests
description: Find properties that must always hold in the code (round-trip, invariants, idempotency, equivalence) and write property-based tests for them with fast-check, Hypothesis, proptest or the ecosystem's equivalent. Use when the user asks for property tests or fuzz-style tests, when hardening parsers, serializers, money/state logic, migrations or rewrites, or when example-based tests feel like they only cover the cases the author already thought of.
---

# property-tests

Example-based tests check what the author thought might go wrong. Property tests generate thousands of inputs that try to break a statement you believe can't fail — catching the edge cases agents (and people) tend to miss, without sharing the bias of whoever wrote the code.

## 1. Pick the library

| Language | Library |
|---|---|
| JS / TS | [`fast-check`](https://fast-check.dev/) |
| Python | [`hypothesis`](https://hypothesis.readthedocs.io/en/latest/) |
| Rust | [`proptest`](https://proptest-rs.github.io/proptest/) (or [`quickcheck`](https://github.com/BurntSushi/quickcheck)) |
| Go | [`testing/quick`](https://pkg.go.dev/testing/quick), [`rapid`](https://github.com/flyingmutant/rapid) |
| Java / Kotlin | [`jqwik`](https://jqwik.net/), [`kotest-property`](https://kotest.io/docs/proptest/property-based-testing.html) |
| Elixir | [`StreamData`](https://hexdocs.pm/stream_data/) |
| Swift | [`SwiftCheck`](https://github.com/typelift/SwiftCheck) |

Use the one already in the project if present. Otherwise add it as a dev dependency and wire it into the existing test runner.

## 2. Hunt for properties

Scan the target code (or the diff) for these shapes:

- **Round-trip** — `decode(encode(x)) == x`. Parsers/printers, serializers, URL/query builders, date formatting, compression, DB mappers.
- **Invariants** — something that must always be true. "Balance is never negative", "list stays sorted", "total equals sum of line items", "no duplicate IDs".
- **Idempotency** — doing it twice equals doing it once. Migrations, normalizers, retries, `upsert`, cache warmers, formatters.
- **Equivalence (oracle)** — optimized code matches a slow but obviously correct version, or new code matches old code.
- **Commutativity / order independence** — merge, set operations, event reducers where order shouldn't matter.
- **Bounds** — output length, value range, monotonicity ("adding an item never lowers the total").

List candidates with a one-line statement each and confirm the important ones with the user if the domain rule isn't evident from the code.

## 3. Write good generators

- Generate the **real input domain**, including empty, huge, unicode, negative, zero, boundary and malformed values.
- Constrain only where the function's contract requires it; over-constrained generators hide bugs.
- Build domain objects from smaller generators rather than fixtures.

## 4. Write the tests

- One property per test, named after the statement (`roundTripsAnyValidInvoice`).
- Keep the default run fast (e.g. 100–1000 cases); allow a higher count via env var for CI or nightly.
- Make failures reproducible: log or pin the seed, and let the library shrink to a minimal counterexample.

### Example: Python with Hypothesis

```python
# conftest.py — fast by default, thorough in CI: HYPOTHESIS_PROFILE=ci pytest
import os
from hypothesis import settings

settings.register_profile("default", max_examples=200)
settings.register_profile("ci", max_examples=2000, print_blob=True)
settings.load_profile(os.getenv("HYPOTHESIS_PROFILE", "default"))
```

```python
# test_invoice.py
from decimal import Decimal
from hypothesis import given, example, strategies as st

from invoice import Invoice, LineItem, parse_invoice, serialize_invoice

money = st.decimals(min_value=0, max_value=10**6, places=2)
line_items = st.builds(LineItem, name=st.text(), quantity=st.integers(0, 1000), unit_price=money)
invoices = st.builds(Invoice, items=st.lists(line_items, max_size=50))

@given(invoices)
def test_round_trips_any_invoice(inv):
    assert parse_invoice(serialize_invoice(inv)) == inv

@given(invoices)
@example(Invoice(items=[]))  # a counterexample found earlier, kept as a permanent regression
def test_total_equals_sum_of_line_items(inv):
    assert inv.total == sum((i.quantity * i.unit_price for i in inv.items), Decimal(0))
```

Notes:
- `st.builds(...)` composes domain objects from smaller strategies; `st.text()` already includes unicode and empty strings.
- Hypothesis shrinks failures automatically and replays them from its local example database (`.hypothesis/`). Add `.hypothesis/` to `.gitignore`; keep important counterexamples with `@example` instead.
- `print_blob=True` prints a `@reproduce_failure(...)` line in CI output that reproduces the exact failing case locally.
- See the [Hypothesis docs](https://hypothesis.readthedocs.io/en/latest/) for stateful testing (`RuleBasedStateMachine`), which fits invariants over sequences of operations.

## 5. When a property fails

1. Read the shrunk counterexample.
2. Decide: is the **code** wrong, or is the **property** wrong? Never loosen the property just to go green — if the property was wrong, say why.
3. Fix the code, then add the counterexample as a permanent example-based regression test.

## 6. Report

List each property, its status, any counterexamples found and fixed, and properties you considered but skipped (and why).
