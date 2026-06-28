---
force: must
why:
  - design/020-goals.kb/drive-by-friendly.md
  - design/020-goals.kb/disposable-components.md
---

# No version lockstep

Versions **must** float per component — language/toolchain versions, third-party
dependencies, and your own libraries each pin independently. There **must not**
be a fleet-wide lockstep requirement, with the sole exception of the build tool
itself (the buck2 binary, whose prelude is bundled).

Non-negotiable: "everything must be on the same version" is the hell this
architecture exists to avoid.

Descriptive rationale: `/discourse.kb/claims.kb/no-infra-lockstep-needed.md`,
`.../toolchains-float-via-package-modifiers.md`,
`.../prelude-bundled-in-binary.md`.
