---
status: asserted
kind: entailment
conclusion: claims.kb/no-infra-lockstep-needed.md
premises:
  - claims.kb/prelude-bundled-in-binary.md
  - claims.kb/toolchains-float-via-package-modifiers.md
likelihood: 0.9
tags: [buck2, composition, lockstep]
---

# Why composition needs no shared infra lockstep

The "infra cell" was two things. The prelude is bundled in the binary, so it is
not a vendored cell at all (claims.kb/prelude-bundled-in-binary.md). Toolchain
versions are set by directory-scoped PACKAGE modifiers that travel with each
repo's subtree, so they compose without a shared pin
(claims.kb/toolchains-float-via-package-modifiers.md). With both "infra"
components removed from the must-share set, nothing remains to fleet-pin except
the buck2 binary version itself — a single tool pin. Hence no shared infra
lockstep.
