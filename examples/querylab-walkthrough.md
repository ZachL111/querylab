# Querylab Walkthrough

I use this file as a small checklist before changing the SQL implementation.

| Case | Focus | Score | Lane |
| --- | --- | ---: | --- |
| baseline | index fit | 171 | ship |
| stress | join width | 177 | ship |
| edge | constraint risk | 158 | ship |
| recovery | plan drift | 200 | ship |
| stale | index fit | 229 | ship |

Start with `stale` and `edge`. They create the widest contrast in this repository's fixture set, which makes them better review anchors than the middle cases.

The next useful expansion would be a malformed fixture around join width and plan drift.
