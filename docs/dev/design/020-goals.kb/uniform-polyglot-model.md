---
why:
  - 010-mission.kb/polyglot-self-similar-template.md
---

# Goal: uniform polyglot model

**One** composition model and **one** mental model across every language. A
package is declared, depended upon, built, tested, and composed the same way
whether it is Python, Rust, or JS — and the same way at every level of nesting.

This is what rules out per-ecosystem sprawl (configuring uv _and_ pnpm _and_
cargo workspaces separately, each with its own composition story) and what
motivates a single cross-ecosystem build spine. It is the goal that
`self-similar`, `dependencies-stay-a-dag`, and `homogeneity-and-robustness`
serve.
