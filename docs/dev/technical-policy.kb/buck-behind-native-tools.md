---
force: must
why:
  - design/020-goals.kb/drive-by-friendly.md
---

# buck stays behind native tools

buck **must never** be required of a drive-by contributor. Native ecosystem
tools (uv / pnpm / cargo) **must** remain a _sufficient_ build for the
contributor loop; generated BUCK files **must** be treated as non-editable
(git-ignored or committed read-only); and CI **should** prove buck and native
builds agree (dual-CI equivalence).

buck is the unifying spine for _maintainers_ and cross-language composition —
but it sits behind the native surface, never in front of it.

Non-negotiable: the day the repo becomes buck-only-buildable, drive-by
friendliness is lost.

Descriptive rationale:
`/discourse.kb/claims.kb/drivebys-native-via-buckify-dual-ci.md`,
`/discourse.kb/claims.kb/buck-is-unifying-spine.md`.
