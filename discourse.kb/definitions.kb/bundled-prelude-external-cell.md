---
term: bundled prelude
aliases: [external cell, "[external_cells] prelude = bundled"]
domain: buck2
broader: buckify.md
related: [buckify.md]
tags: [buck2, prelude, external-cells]
---

# Bundled prelude (external cell)

A buck2 cell whose source is not checked into the repo. The prelude's `bundled`
origin embeds it in the buck2 binary, version-matched to it.

Why it matters here: it dissolves the (mistaken) notion of a shared "infra cell"
that N composed repos must keep in lockstep. There is nothing to vendor; the
prelude is whatever the invoking buck2 binary carries. The only thing common to
a composition is therefore the **buck2 binary version** — a single tool pin like
uv/cargo/pnpm, not a maintained cell.
