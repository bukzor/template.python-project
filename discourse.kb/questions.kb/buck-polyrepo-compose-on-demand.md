---
resolved: claims.kb/compose-on-demand-generated-view.md
sources: [sources.kb/design-chat-2026-06.md]
depends: [questions.kb/does-composition-need-infra-lockstep.md]
tags: [buck2, polyrepo, composition]
---

# Can I have little buck repos and compose them into a super-repo at will?

bukzor rejected both a real monorepo and the submodule "tree" constraint (not
self-similar; deps are a DAG not a tree), and disliked josh (shared history
defeats deletable per-component histories).

Resolved **yes** via compose-on-demand
(claims.kb/compose-on-demand-generated-view.md): the super-repo is a generated,
disposable view assembled from leaf repos as buck cells. Pending one cell-alias
spike. The submodule-as-cell mechanism works but its dual-context tax is what
the generated-view approach minimizes.
