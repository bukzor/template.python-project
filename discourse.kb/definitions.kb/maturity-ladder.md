---
term: code maturity ladder
aliases: [four levels, apps/lib/packages ladder, promotion ladder]
domain: monorepo architecture
related: [self-similar-repo.md, hosting-contract.md]
tags: [monorepo, maturity, apps, lib, packages]
---

# Code maturity ladder

bukzor's four levels of maturity for a piece of code, mapped to repo location:

1. **single-purpose** (`apps/`) — a DAG _sink_; consumed by nobody.
2. **reused** (`lib/python/`) — imported by 2+ consumers in one repo;
   **unpackaged** (no manifest, path/namespace import).
3. **packaged** (`packages/{ecosystem}/`) — has a manifest; a declarable,
   versionable dependency; consumers still in-repo.
4. **published** — own home / registry; depended on across repos / externally.

Two invariants surfaced:

- The **only boundary-crossing promotion is 3→4** (publish). Levels 1–3 are
  within-repo maturity.
- **You cannot export below level 3**: unpackaged code has no version/interface
  to depend on, so `lib/python` is necessarily single-repo. The ladder and the
  repo boundary are the same line.

Minor: "published" (audience) is slightly orthogonal to apps-vs-lib (reuse) — a
CLI _app_ can also be published.
