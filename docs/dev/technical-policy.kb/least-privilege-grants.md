---
force: should
why:
  - design/020-goals.kb/disposable-components.md
---

# Least-privilege permission grants

Every unit that grants authority — a CI workflow's trusted-publisher identity, a
token's scopes, a service account's roles — **should** carry the narrowest grant
that still works, and a broad capability **should** split into many small
single-purpose units rather than pool into one. A grant's blast radius on
compromise is exactly its scope.

`should`, not `must`: a justified local exception is allowed when splitting
costs more than the narrowed blast radius returns — but the default splits.

Instantiation (GitHub Actions → PyPI / npm): the **workflow file is the RBAC
unit** — a trusted publisher binds `(owner, repo, workflow-file, environment)`,
so whoever can edit that file holds its publish rights. Therefore one registry
per workflow (`release-pypi.yml`, `release-npm.yml`), never a shared
`release.yml`; shared build/coordination factors into reusable workflows, which
keeps things DRY without widening the grant.
