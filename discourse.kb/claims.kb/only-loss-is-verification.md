---
status: asserted
likelihood: 0.85
date-observed: 2026-06-24
tags: [buck2, polyrepo, verification, blast-radius]
depends:
  [
    definitions.kb/stutter-step.md,
    claims.kb/compose-on-demand-generated-view.md,
  ]
---

# The only real loss without repo-spanning buck is verified (vs. trusted) non-breakage

Three cross-boundary source operations are "lost" with per-repo buck, but only
one genuinely survives mitigation:

1. **fast inner-loop co-dev across repos** — mitigated by native path-overrides
   (uv sources / cargo patch / pnpm link); works but escapes buck.
2. **global blast-radius verification** — the real loss. A monorepo _proves_ no
   consumer breaks before merge; across repos you _trust_ the stutter-step
   discipline and find breakage late, in someone else's CI. Discipline ≠ proof.
3. **atomic cross-boundary refactor** — designed away: such things should be one
   repo (the miscategorization signal).

So "losing buck's full power" reduces to loss #2. And even #2 is recoverable
**on demand**: an ephemeral CI job that composes the library + its consumers at
its branch SHA and runs their buck tests — the same compose-on-demand machinery,
used transiently. You pay for repo-spanning buck only when you want it.

Answers `questions.kb/cost-of-no-repo-spanning-buck.md`.
