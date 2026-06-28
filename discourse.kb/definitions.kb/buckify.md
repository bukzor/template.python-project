---
term: buckify
domain: build systems
related: [bundled-prelude-external-cell.md]
tags: [buck2, buckify, third-party, codegen]
---

# Buckify

Generating BUCK build files from native package-manager configuration. Two
layers, with different difficulty:

- **Third-party**: read a native lockfile, emit BUCK targets. Mature for cargo
  (reindeer); DIY for python/uv; roughest for npm/pnpm.
- **First-party**: emit BUCK targets for _your own_ packages from their
  manifest. Feasible while a package is "boring" (manifest + `src/` glob); stops
  being generatable once you use buck's distinctive power (custom genrules,
  codegen, cross-language deps), which forces hand-written BUCK.

In this design buckify is the mechanism that keeps drive-by contributors on
native tools: native manifests stay the source of truth, BUCK is generated and
treated as non-editable (gitignored, or committed read-only).
