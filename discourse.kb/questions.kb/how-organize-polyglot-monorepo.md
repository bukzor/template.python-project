---
resolved: claims.kb/maturity-ladder-resolves-organization.md
sources: [sources.kb/design-chat-2026-06.md]
depends: [questions.kb/is-monorepo-relevant-to-project-type.md]
tags: [monorepo, apps, lib, packages, maturity]
---

# How should the polyglot monorepo be organized?

Resolved by the **apps/lib/packages maturity ladder + hosting contract**
(claims.kb/maturity-ladder-resolves-organization.md): `apps/` (single-purpose),
`lib/python/*` (reused, unpackaged), `packages/{ecosystem}/*` (packaged),
promotion to published as level 4 — self-similar and DAG-respecting, with the
unpackaged-vs-packaged line as the load-bearing distinction.
