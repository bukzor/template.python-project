---
status: asserted
likelihood: 0.95
date-observed: 2026-06-25
tags: [buck2, prelude, external-cells]
sources: [sources.kb/buck2-external-cells.md]
depends: [definitions.kb/bundled-prelude-external-cell.md]
---

# The prelude is bundled in the buck2 binary — there is no infra cell to vendor

With `[external_cells] prelude = bundled`, the prelude's source lives inside the
buck2 binary, version-matched to it. So the only thing common to a composition
is **which buck2 binary you invoke** — a single tool pin (launcher +
`.buck2version`-style file), exactly like pinning uv/cargo/pnpm. Nothing to
vendor, nothing to sync across N repos.

A specific prelude can still be frozen per-repo via a `git` external-cell
`commit_hash` if ever needed.
