---
force: should
why:
  - design/020-goals.kb/uniform-polyglot-model.md
---

# Homogeneity and robustness

Prefer **one** homogeneous, robust way to do a thing across the whole repo over
per-case variation — solve it once, for everyone, in a way that holds up. When a
hard problem (e.g. cross-context toolchain consistency) admits a uniform
solution designed with care, that is preferred over N bespoke workarounds.

`should`, not `must`: a deliberate, justified local exception is allowed when
homogeneity would cost more than it returns — but the default leans uniform.

This is the bukzor working value ("solvable by me, for me, homogeneous and
robust") applied to architecture.
