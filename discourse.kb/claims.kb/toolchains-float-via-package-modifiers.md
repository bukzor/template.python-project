---
status: asserted
likelihood: 0.9
date-observed: 2026-06-25
tags: [buck2, toolchains, modifiers, versions]
sources: [sources.kb/buck2-modifiers-toolchains.md]
---

# Language/toolchain versions float per repo via directory-scoped PACKAGE modifiers

A single toolchain target uses `select()` on a `python_version` constraint;
**directory-scoped `PACKAGE`-file modifiers** drive which version applies where.
Because each composed repo carries its own `PACKAGE` file in its own subtree,
per-repo versions **compose automatically** — repo A on py3.11 and repo B on
py3.13 in one build is idiomatic, not a hack.

This grants bukzor's "just have libraries at whatever version they're at" for
the _toolchain_ dimension: no fleet lockstep on language versions. (Third-party
lib versions also float, as distinct per-repo cells.)
