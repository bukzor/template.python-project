---
status: retracted
likelihood: 0.1
date-observed: 2026-06-24
tags: [buck2, retracted]
depends: [claims.kb/buck-is-unifying-spine.md]
---

# (RETRACTED) buck is an optional accelerator atop native workspaces

**Retracted 2026-06-25.** Original (wrong) position: build the native substrate
(uv/pnpm/cargo workspaces) first, treat buck as an optional accelerator added
last for incrementality/scale.

Flaw: it modeled buck as a _performance layer_ over per-ecosystem workspaces.
But those workspaces are single-ecosystem islands with no cross-language
composition or self-similarity story
(claims.kb/native-workspaces-single-ecosystem.md). So "native first, buck
optional" prescribes exactly the per-ecosystem sprawl buck exists to delete.
buck is the spine, not an accessory.

Superseded by claims.kb/buck-is-unifying-spine.md. See
deductions.kb/retraction-of-optional.md.
