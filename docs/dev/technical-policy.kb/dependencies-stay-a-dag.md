---
force: must
why:
  - design/020-goals.kb/uniform-polyglot-model.md
---

# Dependencies stay a DAG

The dependency graph **must** be modeled as a DAG and **must not** be forced
into a tree. Source _ownership_ may be a forest (each artifact has one canonical
home), but that is a separate graph from _dependency_ — conflating them (e.g. a
"submodules must form a tree" rule) is prohibited.

Non-negotiable: this is how software actually composes; a model that imposes a
tree on dependencies is rejected on sight.

Descriptive rationale:
`/discourse.kb/claims.kb/dependency-dag-vs-ownership-forest.md`.
