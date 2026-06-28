---
status: asserted
likelihood: 0.85
date-observed: 2026-06-25
tags: [buck2, third-party, python, node, cargo, risk]
sources: [sources.kb/buck2-oss-thirdparty-roughness.md, sources.kb/reindeer.md]
---

# Third-party importers remain per-ecosystem — the open maturity risk

buck unifies first-party structure and composition, but **third-party resolution
stays per-ecosystem**: a separate generated importer per ecosystem. Maturity is
uneven in OSS buck2:

- **cargo**: paved (reindeer).
- **python/uv**: DIY (no first-class importer).
- **npm/pnpm**: roughest (internal Meta js/node rules; no documented OSS pnpm
  third-party flow).

This is the concrete risk on the buck-as-spine bet
(claims.kb/buck-is-unifying-spine.md): the unification is real for first-party +
build interface, but the per-ecosystem third-party leaves are where the real
effort/uncertainty lives — and they are roughest for exactly the ecosystems
bukzor leans on (python, pnpm).
