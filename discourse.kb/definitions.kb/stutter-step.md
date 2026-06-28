---
term: forward-compatibility stutter step
aliases: [stutter-step discipline, semver bridge]
domain: library versioning
related: [hosting-contract.md]
tags: [libraries, semver, versioning, migration]
---

# Forward-compatibility stutter step

bukzor's discipline: every forward-incompatible library change ships a
**forward-compatible bridge first** — add the new alongside the old, deprecate,
then remove across two releases — so consumers migrate **asynchronously**.

Load-bearing role: a well-behaved library therefore _never_ forces an atomic
cross-repo change. This is what makes artifact-boundary (published) cross-repo
dependencies painless, and it is why the "atomic cross-cutting change" cost of
polyrepo lands only on things that were miscategorized — if you _need_ an atomic
cross-repo edit, the pieces are one app and belong in one repo.

It is a **cultural** invariant: a template can document it but cannot enforce
it.
