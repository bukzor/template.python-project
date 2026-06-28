---
status: asserted
likelihood: 0.9
date-observed: 2026-06-25
tags: [buck2, composition, lockstep, infra]
depends:
  [
    claims.kb/prelude-bundled-in-binary.md,
    claims.kb/toolchains-float-via-package-modifiers.md,
  ]
---

# Composition needs no shared fleet-pinned "infra cell"

An earlier claim that composed repos must share a fleet-pinned prelude/toolchain
cell was wrong, on two counts:

1. the **prelude is bundled in the buck2 binary**, not a vendored cell
   (claims.kb/prelude-bundled-in-binary.md);
2. **language/toolchain versions float per-repo** via directory-scoped PACKAGE
   modifiers (claims.kb/toolchains-float-via-package-modifiers.md).

So everything that is a _version_ (languages, third-party, your libraries)
floats per repo. The lone common element is the **buck2 binary version** — one
tool pin like uv/cargo/pnpm.

Residual soft coupling: the composing binary's bundled prelude must satisfy
every composed repo's BUCK API usage — trivially true on a current binary,
occasionally a small migration if one repo lags; pinnable via git external-cell
if ever needed. Far softer than "fleet-pinned infra cell."

Answers `questions.kb/does-composition-need-infra-lockstep.md`.
