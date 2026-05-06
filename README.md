# querylab

`querylab` is a compact SQL repository for databases, centered on this goal: Package relational fixtures and sqlite3 checks for query correctness.

## Purpose

This is intentionally local and self-contained so it can be inspected without credentials, services, or seeded history.

## Querylab Review Notes

The first comparison I would make is `index fit` against `constraint risk` because it shows where the rule is most opinionated.

## What Is Covered

- `fixtures/domain_review.csv` adds cases for index fit and join width.
- `metadata/domain-review.json` records the same cases in structured form.
- `config/review-profile.json` captures the read order and the two review questions.
- `examples/querylab-walkthrough.md` walks through the case spread.
- The SQL code includes a review path for `index fit` and `constraint risk`.
- `docs/field-notes.md` explains the strongest and weakest cases.

## Implementation Notes

The implementation keeps the scoring rule plain: reward signal and confidence, preserve slack, penalize drag, then classify the result into a review lane.

The SQL checks add a separate view over the domain review fixture.

## Command

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File scripts/verify.ps1
```

## Audit Path

The same command runs the local verification path. The highest-scoring domain case is `stale` at 229, which lands in `ship`. The most cautious case is `edge` at 158, which lands in `ship`.

## Limits

The fixture set is small enough to audit by hand. The next useful expansion is malformed input coverage, not extra surface area.
