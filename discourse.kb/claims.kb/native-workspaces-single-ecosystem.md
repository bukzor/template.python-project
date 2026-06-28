---
status: asserted
likelihood: 0.97
date-observed: 2026-06-25
tags: [uv, pnpm, cargo, workspace, polyglot]
depends: [definitions.kb/self-similar-repo.md]
---

# Native workspaces are single-ecosystem islands

uv workspaces compose Python packages, pnpm composes JS, cargo composes Rust.
**None composes across languages**, and none gives a uniform cross-language
package shape. There is no native primitive for "this repo has python + rust +
js packages; compose them into one graph with cross-language deps."

The whole category of polyglot monorepo tools (buck2, Bazel, Pants, Please, Nx)
exists _because_ native package managers are single-ecosystem. Faking
cross-ecosystem composition with scripts/make is bespoke per-repo glue — the
opposite of self-similar.
