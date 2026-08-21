---
force: must
why:
  - design/020-goals.kb/disposable-components.md
  - design/020-goals.kb/drive-by-friendly.md
---

# A release is built once and is immutable

A release artifact **must** be built once and promoted **unchanged** (the same
bytes) through every environment — never rebuilt per environment. A published
artifact **must** be immutable: a given version **must not** ever resolve to two
different artifacts.

`ensure-published` (`get-require-ensure-verbs.md`) enforces this: absent →
publish; byte-identical → no-op; **present-but-different → hard error**. The git
tag is the **commit point**, written **last**, as the record that a release
succeeded — so a crash mid-release leaves a recoverable, detectable state, not a
silent inconsistency. `reconcile` audits tag <-> package <-> green-CI drift in
both directions and is the layer that catches violations a gate let through.

Only the release pipeline may publish — no human hand-publish — or every other
guarantee here is bypassable. This refines
`cross-repo-via-published-artifact.md` (the artifact is the boundary) and rides
on `least-privilege-grants.md` (one narrowly-scoped publisher per registry).

Non-negotiable: mutable or hand-made releases break the correspondence between a
SHA, its CI verdict, and what users actually receive.
