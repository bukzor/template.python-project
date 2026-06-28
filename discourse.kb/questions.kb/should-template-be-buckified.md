---
resolved: claims.kb/buck-is-unifying-spine.md
sources: [sources.kb/design-chat-2026-06.md]
depends:
  - questions.kb/how-organize-polyglot-monorepo.md
  - questions.kb/keep-drivebys-buck-unaware.md
tags: [buck2, template, direction]
---

# Should template.python-project be buckified?

The landing question. Resolved **yes** — buck2 is the load-bearing unifying
spine for a polyglot, self-similar, composable repo template
(claims.kb/buck-is-unifying-spine.md), because native workspaces cannot compose
across ecosystems. Native package managers are preserved as per-package leaves
and the drive-by build surface; buck is the cross-ecosystem composition layer
over them.

Concrete next step in claims.kb/buckify-repo-as-python-node-proof.md (buckify
this repo as a Python+Node proof; rename; write the convention/ADR doc).

Open risk tracked in claims.kb/third-party-importers-remain-per-ecosystem.md.
