---
status: asserted
likelihood: 0.8
date-observed: 2026-06-25
tags: [buck2, polyrepo, composition, cells]
depends:
  [
    claims.kb/no-infra-lockstep-needed.md,
    definitions.kb/bundled-prelude-external-cell.md,
  ]
sources: [sources.kb/buck2-external-cells.md]
---

# Little buck repos compose into a super-repo on demand — generated, not maintained

The super-repo is **materialized from the little repos when cross-repo buck is
wanted, then discarded** — the leaves stay the source of truth. A composition
generator assembles checked-out repos (each a cell) under a generated root
`.buckconfig`.

Discipline that makes any subset composable:

- shared infra (prelude/toolchains) needs no vendored cell — see
  claims.kb/no-infra-lockstep-needed.md;
- **intra-repo references use bare `//` (current cell), never the repo's own
  cell name** — the linchpin for standalone-and-composed portability;
- **third-party stays per-repo cells** (independent versions coexist as distinct
  cells; no diamond to reconcile).

Same tool serves the blast-radius recovery
(claims.kb/only-loss-is-verification.md), co-development, and atomic cross-repo
refactors.

One spike before betting: confirm buck2's cell-alias reconciliation with a
two-repo toy (standalone + composed both build). likelihood 0.8 pending that
spike.

Answers `questions.kb/buck-polyrepo-compose-on-demand.md`.
