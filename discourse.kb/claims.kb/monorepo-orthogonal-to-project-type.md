---
status: asserted
likelihood: 0.95
date-observed: 2026-06-24
tags: [project_type, monorepo, copier]
---

# Monorepo/workspace structure is orthogonal to project_type (app|lib)

`project_type` is two independent axes:

1. **root package shape** — app (runnable, no build-system, root `main.py`) vs.
   lib (installable, hatchling build-system, `src/{slug}/`);
2. **multi-package substrate** — whether the repo is a workspace with member
   sub-packages.

These don't constrain each other; the full 2×2 is valid. Proven in the wild by
this very repo, which is app-shaped at root yet already carries `lib/`
sub-packages (`lib/ci`, `lib/local-devenv`). So the workspace/monorepo substrate
sits _beneath both_ branches.

Reframe this unlocks: `project_type` shrinks to "where the primary package
lands" — `apps/{slug}` vs `packages/pypi/{slug}` — with the root as a pure
coordinator. `local-devenv` relocates to `packages/pypi/local-devenv` (it has a
manifest → ladder level 3).

Answers `questions.kb/is-monorepo-relevant-to-project-type.md`.
