---
kind: standard
title: "Buck2 docs — External Cells (bundled prelude)"
url: https://buck2.build/docs/users/advanced/external_cells/
tags: [buck2, prelude, external-cells, toolchains]
---

# Buck2 External Cells

The prelude can be an _external cell_ with `bundled` origin
(`[external_cells] prelude = bundled`) — its source is embedded in the buck2
binary, version-matched to it, not checked into the repo. A specific prelude can
instead be pinned via a `git` origin with a `commit_hash`, or expanded into the
repo with `expand-external-cell`.

Consequence used in this graph: there is **no checked-in "infra cell" to vendor
or keep N repos in lockstep on** — the prelude rides inside whichever buck2
binary performs the build.
