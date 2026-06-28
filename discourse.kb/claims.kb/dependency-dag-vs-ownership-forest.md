---
status: asserted
likelihood: 0.95
date-observed: 2026-06-24
tags: [dependencies, dag, ownership, polyrepo]
depends: [definitions.kb/hosting-contract.md]
---

# Dependency graph (DAG) and ownership graph (forest) are different graphs

The "must it be a tree?" confusion came from conflating two graphs:

- **Dependency graph**: a DAG. Always. B may be depended on by many.
- **Ownership graph** (who is the canonical _home_ of source): a **forest** —
  each artifact has exactly one home.

A DAG of dependencies over a forest of ownership is exactly how every registry
works (crates.io = single-home namespace; the crate dep graph atop it is an
arbitrary DAG). This dissolves both of bukzor's objections to an earlier
"submodules must form a tree" rule: the tree constraint belongs to _ownership_,
not _dependency_, and applying it uniformly (top repo = its parts) makes it
self-similar.
