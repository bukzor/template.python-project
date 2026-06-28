---
status: asserted
kind: entailment
conclusion: claims.kb/buck-is-unifying-spine.md
premises:
  - claims.kb/native-workspaces-single-ecosystem.md
  - definitions.kb/self-similar-repo.md
likelihood: 0.85
tags: [buck2, polyglot, spine]
---

# Why buck is the spine

The goal is a polyglot, self-similar, composable repo template. Self-similarity
and cross-language composition require a primitive that is uniform across
ecosystems. Native workspaces are single-ecosystem islands
(claims.kb/native-workspaces-single-ecosystem.md), so they cannot supply it.
buck2 (the polyglot-build-system category) is the only available primitive that
does. Therefore buck is load-bearing for the goal — the spine — not an optional
accelerator. The residue (per-ecosystem third-party importers) does not touch
the first-party composition/self-similarity that the conclusion claims.
