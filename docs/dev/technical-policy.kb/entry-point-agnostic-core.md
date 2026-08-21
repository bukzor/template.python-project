---
force: should
why:
  - design/020-goals.kb/drive-by-friendly.md
  - design/020-goals.kb/uniform-polyglot-model.md
---

# Workflow logic lives in an entry-point-agnostic core

CI/CD logic **should** live in small portable scripts that a human _or_ a robot
can run with sufficient permission — not in the workflow UI (GitHub Actions
YAML, `make`, cron). The entry point **should** do nothing but supply a commit
SHA and credentials and call **one** verb; every trigger funnels into the same
verb (`release <sha>`), so a maintainer at a terminal and CI exercise the
identical path.

Agnostic as far as possible, and no further. Four concerns are irreducibly
platform-specific and **must** be the _only_ things that vary across entry
points: context discovery (which SHA/ref, is this a PR), credential acquisition,
the check-status query, and the trigger itself. Quarantine them
(`platform-isolated-in-providers.md`); everything downstream consumes their
normalized output and stays portable.

`should`, not `must`: a thin platform-only step (e.g. minting an OIDC token) may
sit in the entry point when wrapping it buys nothing — but logic does not.

This is `homogeneity-and-robustness.md` applied to delivery: one way to release,
reachable from every context.
