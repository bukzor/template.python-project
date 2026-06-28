---
kind: standard
title: "Buck2 docs — Configuration Modifiers & Writing Toolchains"
url: https://buck2.build/docs/concepts/modifiers/
tags: [buck2, toolchains, modifiers, configuration, select]
---

# Buck2 Modifiers & Toolchains

A single toolchain target uses `select()` on constraints (e.g. a
`python_version` setting); **directory-scoped modifiers in `PACKAGE` files**
drive which value applies where — "a modifier in `foo/PACKAGE` covers all
targets in `foo/…`". Also settable per-target and per-CLI-invocation.

Consequence used in this graph: because modifiers are directory-scoped and each
composed repo carries its own `PACKAGE` file, **per-repo language/toolchain
versions compose automatically** with no shared pin. Mixed Python versions in
one build is idiomatic, not a hack.

See also: https://buck2.build/docs/rule_authors/writing_toolchains/
