---
kind: testimony
title:
  "Design conversation — buck2 as polyglot unifier for template.python-project"
authors: [bukzor, claude-opus-4-8]
date-published: 2026-06-25
tags: [buck2, monorepo, polyrepo, template, polyglot]
---

# Design chat, 2026-06-24/25

Working session that started from the `project_type: app|lib` copier task and
expanded into the full direction of the template. Key moves, in order:

1. `project_type` is really two orthogonal axes (root package shape vs.
   workspace/multi-package substrate).
2. bukzor's three-way monorepo split (`apps/ lib/ packages/{ecosystem}/`) and
   the four-level maturity ladder.
3. buck2's interplay with uv/pnpm/cargo; drive-by friendliness; polyrepo vs.
   monorepo; compose-on-demand; what is lost without repo-spanning buck.
4. Correction: buck2 is not an optional accelerator on top of native workspaces
   — it is the _only_ cross-ecosystem composition + self-similarity primitive,
   hence the load-bearing spine.

bukzor's standing requirements surfaced here: drive-by contributors must never
need to learn buck; deletable per-component histories are valued; toolchain
homogeneity is acceptable but library/toolchain _versions_ should float.
