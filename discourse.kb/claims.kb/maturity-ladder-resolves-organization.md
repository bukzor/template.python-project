---
status: asserted
likelihood: 0.9
date-observed: 2026-06-24
tags: [monorepo, apps, lib, packages, maturity]
depends:
  [
    definitions.kb/maturity-ladder.md,
    definitions.kb/hosting-contract.md,
    claims.kb/dependency-dag-vs-ownership-forest.md,
  ]
---

# The apps/lib/packages maturity ladder + hosting contract organize the monorepo

bukzor's structure: `apps/` (single-purpose), `lib/python/*` (reused,
unpackaged), `packages/{ecosystem}/*` (packaged), with promotion to "published"
as level 4. The load-bearing distinction is **unpackaged `lib/python` vs.
packaged `packages/{eco}`** — most "little side packages cut for trivia" want
zero-ceremony `lib/python`, graduating only when they need real
deps/build/publish.

The hosting contract governs boundaries: cross-repo dependency only via
published artifact. Combined, this is **self-similar** (one rule at every level)
and **DAG-respecting**. The `{ecosystem}` dir (pypi/cargo/npm/…) keeps the
glob-listable invariant and reserves room for future languages.

Answers `questions.kb/how-organize-polyglot-monorepo.md`.
