---
resolved: claims.kb/no-infra-lockstep-needed.md
sources:
  [
    sources.kb/design-chat-2026-06.md,
    sources.kb/buck2-external-cells.md,
    sources.kb/buck2-modifiers-toolchains.md,
  ]
tags: [buck2, composition, lockstep, toolchains]
---

# Does composing buck repos require a shared fleet-pinned infra cell?

bukzor's objection: a fleet-pinned infra cell sounds like fresh hell — "can't we
just have libraries at whatever version they're at?"

Resolved **no** (claims.kb/no-infra-lockstep-needed.md): the prelude is bundled
in the buck2 binary (not a vendored cell), and toolchain versions float per-repo
via directory-scoped PACKAGE modifiers. The only common element is the buck2
binary version — one tool pin. An earlier "fleet-pinned infra cell" claim was a
mental-model error and is corrected here.
