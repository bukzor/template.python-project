---
force: must
why:
  - design/020-goals.kb/uniform-polyglot-model.md
---

# Self-similar structure

The repo layout (`apps/ lib/python/ packages/{ecosystem}/`) **must** be
identical at every level of nesting. An app may contain its own
`apps/lib/packages`, and the top repo obeys the **same** rule as its parts —
there is no special "the monorepo vs. its parts" rule.

Non-negotiable: a design with a distinct top-level rule fails this outright.

Descriptive rationale: `/discourse.kb/definitions.kb/self-similar-repo.md` —
note that self-similarity over flat native workspaces is layout-only (no
isolation); genuine per-level isolation requires the buck spine.
