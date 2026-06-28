---
status: asserted
kind: entailment
conclusion: claims.kb/compose-on-demand-generated-view.md
premises:
  - claims.kb/no-infra-lockstep-needed.md
  - claims.kb/dependency-dag-vs-ownership-forest.md
  - definitions.kb/bundled-prelude-external-cell.md
likelihood: 0.8
tags: [buck2, composition, cells]
---

# Why compose-on-demand is tractable

A `.buckconfig` marks a cell; nested `.buckconfig`s are nested cells, so each
little repo composes as a cell under a generated super-root. Nothing forces a
shared infra cell (claims.kb/no-infra-lockstep-needed.md), so the only shared
element is the invoking binary. Ownership stays a forest while dependencies form
a DAG (claims.kb/dependency-dag-vs-ownership-forest.md), so per-repo third-party
cells and bare-`//` self-reference let a repo build both standalone and
composed. The super-repo is therefore a disposable generated view, not a
maintained structure — modulo one cell-alias spike. likelihood 0.8 pending that
spike.
