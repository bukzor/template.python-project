---
status: asserted
likelihood: 0.8
date-observed: 2026-06-25
tags: [template, buck2, sequencing, dogfood]
depends:
  [
    claims.kb/buck-is-unifying-spine.md,
    claims.kb/third-party-importers-remain-per-ecosystem.md,
  ]
---

# Next step: buckify this repo as a Python+Node two-language proof

buck's _build-incrementality_ value is nil at single-package scale, but its
_unification_ value appears only at **2+ ecosystems** — and this repo already
ships `package.json`/pnpm alongside Python. So the first concrete move is to
buckify _this_ repo (the dogfooding instance) as a two-language proof:
`.buckconfig` with `[external_cells] prelude = bundled`, a python toolchain + a
node toolchain, and the `apps/lib/packages` convention as uniform BUCK files —
native manifests preserved underneath as per-package leaves and the drive-by
build. Then template it.

Cheap early wins that still stand, reframed around buck-as-spine: **rename the
repo** (python-only is already false) and **write the convention/ADR doc**
(maturity ladder + hosting contract + buck-optional-for-drivebys mechanics).

A single-language buck repo would prove nothing — the thesis (uniform shape,
cross-language deps, one CLI) only shows at 2+ ecosystems.
