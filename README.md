# querylab

`querylab` packages a practical databases exercise in SQL. The emphasis is on deterministic behavior, a small public API, and examples that explain the tradeoffs.

## How I Read Querylab

The useful thing to inspect here is how the same score rule is represented in code, metadata, and examples. If those three pieces disagree, the audit script should make the drift visible.

## Problem Shape

The repository exists to keep a technical idea small enough to reason about. The implementation avoids external dependencies where possible, then uses fixtures to make changes easy to review.

## Main Behaviors

- Models schema shape with deterministic scoring and explicit review decisions.
- Uses fixture data to keep query checks changes visible in code review.
- Includes extended examples for fixture rows, including `surge` and `degraded`.
- Documents constraint behavior tradeoffs in `docs/operations.md`.
- Runs locally with a single verification command and no external credentials.

## Internal Model

The core is a scoring model over demand, capacity, latency, risk, and weight. That keeps schema shape, query checks, and fixture rows in one explicit decision path. The threshold is 182, with risk penalty 6, latency penalty 4, and weight bonus 6. The SQL project uses sqlite fixtures, views, and assertions to keep query behavior inspectable.

## Repository Map

- `tests`: verification harness
- `fixtures`: compact golden scenarios
- `examples`: expanded scenario set
- `metadata`: project constants and verification metadata
- `docs`: operations and extension notes
- `scripts`: local verification and audit commands
- `schema.sql`: sqlite schema and view definitions

## Run It Locally

Use a normal shell with SQL available on `PATH`. The verifier is written as a PowerShell script because the portfolio was assembled on Windows.

## How To Run It

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File scripts/verify.ps1
```

This runs the language-level build or test path against the compact fixture set.

## Validation

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File scripts/audit.ps1
```

The audit command checks repository structure and README constraints before it delegates to the verifier.

## Scenario Walkthrough

`baseline` is the first example I would inspect because it lands on the `review` path with a score of 115. The broader file also keeps `degraded` at -38 and `surge` at 223, which gives the model a useful low-to-high spread.

## Known Edges

The examples cover useful edges, not every edge. A larger version would add malformed-input tests, richer reports, and deeper domain parsers.

## Follow-Up Work

- Add a comparison mode that shows how decisions change when one signal is adjusted.
- Add a loader for `examples/extended_cases.csv` and promote selected cases into the language test suite.
- Add a short report command that prints the score breakdown for a single scenario.
- Add one more databases fixture that focuses on a malformed or borderline input.
