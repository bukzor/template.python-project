---
resolved: claims.kb/only-loss-is-verification.md
sources: [sources.kb/design-chat-2026-06.md]
depends: [questions.kb/buck-polyrepo-compose-on-demand.md]
tags: [buck2, polyrepo, verification, blast-radius]
---

# What is the pain of lacking repo-spanning buck graphs?

Resolved (claims.kb/only-loss-is-verification.md): of three cross-boundary
operations, inner-loop co-dev is escape-hatched (native path-overrides) and
atomic refactor is designed away (one repo). The single residual loss is
**verified vs. trusted non-breakage** — and even that is recoverable on demand
as an ephemeral cross-repo composition CI job.
