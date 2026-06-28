--- # workaround: anthropics/claude-code#13003
depends:
    - Skill(llm-design-kb)
---

# Design tower — polyglot, self-similar repo template

Layered design for the template's architecture. Each layer justifies the one
below via `why:`. Layers present: `010-mission.kb/`, `020-goals.kb/`. The
normative design rules that constrain this design live one level up, in
`../technical-policy.kb/`.

This is the **normative** counterpart (_what we want / the rules_) to the
**descriptive** reasoning (_what's true / what follows_) captured in
`/discourse.kb/`. They cross-reference: policies cite the discourse claims that
justify them; the discourse graph's conclusions are _motivated by_ these goals.

Several of these values are personal architecture convictions that govern more
than this repo — **hoist candidates** for a personal-global design scope once a
second repo needs them.
