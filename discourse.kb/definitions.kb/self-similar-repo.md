---
term: self-similar repo
aliases: [self-similarity, recursive monorepo layout]
domain: monorepo architecture
related: [maturity-ladder.md, hosting-contract.md]
tags: [monorepo, self-similar]
---

# Self-similar repo

A repo whose internal structure (`apps/ lib/ packages/{ecosystem}/`) is the
_same shape at every level of nesting_ — an app may contain its own
`apps/lib/packages`, and the top repo obeys the identical rule as its parts. No
special "the monorepo vs. its parts" rule.

Two clarifications established in the chat:

- Self-similarity over flat native workspaces (uv/cargo/pnpm) is **layout**
  recursion only — single workspace, single resolution, **no isolation**.
- buck2's package/target model restores genuine per-target **isolation** at any
  nesting depth, which is why buck is the mechanism that makes the isolation
  half of self-similarity real.
