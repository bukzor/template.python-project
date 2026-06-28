---
term: hosting contract
aliases: [publish-to-cross-repo contract, containment-vs-publication]
domain: monorepo / polyrepo architecture
related: [maturity-ladder.md, stutter-step.md]
tags: [polyrepo, publishing, dependencies]
---

# Hosting contract

bukzor's rule for when a repo may host code B:

> Repo A may host B iff **either** A contains _all_ references to B (B is
> private to A), **or** A publishes B (external consumers depend on the
> published artifact, never on A's source copy).

Tighter form: **containment never crosses a repo boundary; only published
versions do.** Resolves the "tree vs DAG" objection by separating two graphs:
the **dependency graph is a free DAG**; the **ownership graph is a forest**
(each artifact has one canonical home). A DAG of dependencies over a forest of
ownership — exactly how a package registry works.

"Publish" can bootstrap as a **git tag** (`uv/cargo/pnpm add git+…@v1.2`) — no
registry server required to start.
