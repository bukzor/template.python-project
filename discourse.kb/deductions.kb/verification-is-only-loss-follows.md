---
status: asserted
kind: entailment
conclusion: claims.kb/only-loss-is-verification.md
premises:
  - definitions.kb/stutter-step.md
  - claims.kb/compose-on-demand-generated-view.md
likelihood: 0.85
tags: [buck2, polyrepo, verification]
---

# Why verification is the only residual loss

Of the three cross-boundary source operations: the inner-loop is escape-hatched
by native path-overrides; atomic cross-repo refactor is designed away by the
stutter-step discipline (definitions.kb/stutter-step.md), which guarantees
libraries never force atomic consumer changes. That leaves blast-radius
_verification_ — provably knowing no consumer breaks before merge — as the only
capability the artifact boundary genuinely removes. And compose-on-demand
(claims.kb/compose-on-demand-generated-view.md) recovers even that as an
ephemeral CI job. So the standing loss is "verified vs. trusted," recoverable at
will.
