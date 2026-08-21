---
force: must
why:
  - design/020-goals.kb/disposable-components.md
  - design/020-goals.kb/uniform-polyglot-model.md
---

# CI tooling depends on dev tooling, never the reverse

Release tooling **must** layer in one direction only:

    lib/dev/                    mechanism — dev-usable verbs CI reuses
      <- lib/ci/                policy — gating compositions
        <- lib/ci/providers/<name>/   platform

`lib/ci/` may depend on `lib/dev/`; `lib/dev/` **must not** depend on `lib/ci/`.
A `dev -> ci` dependency fails the build. The layout encodes the rule: a
facility usable outside CI **must** live outside `lib/ci/` (in `lib/dev/`, or
its own domain directory) so a developer can run it directly. (`lib/` itself
holds only directories — each child is a namespace.)

This is `dependencies-stay-a-dag.md` at small scale: a one-way arrow, lintable,
with the cheap-to-run mechanism never trapped behind the policy that consumes
it.

Non-negotiable: a facility only a robot can run rots; the dependency direction
is what keeps the mechanism honest and reusable.
