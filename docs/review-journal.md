# Review Journal

The repository goal stays the same: package relational fixtures and sqlite3 checks for query correctness. This note explains the added review angle.

The local checks classify each case as `ship`, `watch`, or `hold`. That gives the project a small review vocabulary that matches its databases focus without claiming live deployment or external usage.

## Cases

- `baseline`: `index fit`, score 171, lane `ship`
- `stress`: `join width`, score 177, lane `ship`
- `edge`: `constraint risk`, score 158, lane `ship`
- `recovery`: `plan drift`, score 200, lane `ship`
- `stale`: `index fit`, score 229, lane `ship`

## Note

This file is intentionally plain so the fixture remains the source of truth.
