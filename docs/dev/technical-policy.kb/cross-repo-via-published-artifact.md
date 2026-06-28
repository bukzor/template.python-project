---
force: must
why:
  - design/020-goals.kb/disposable-components.md
  - design/020-goals.kb/drive-by-friendly.md
---

# Cross-repo dependency only via published artifact

A dependency **must** cross a repo boundary only as a **published artifact** (a
git tag suffices; a registry is optional). Source containment **must not** cross
a boundary: a repo may host code only if it contains _all_ references to that
code, or publishes it.

Corollary — the maturity ladder's only boundary-crossing promotion is
"published"; and any change that would require an _atomic_ cross-repo edit is
the signal that the pieces belong in one repo. Libraries avoid this by the
forward-compatibility stutter step.

Non-negotiable: it is what keeps the dependency graph a free DAG over a
single-home ownership forest, and what keeps histories disposable.

Descriptive rationale: `/discourse.kb/definitions.kb/hosting-contract.md`,
`/discourse.kb/claims.kb/maturity-ladder-resolves-organization.md`.
