--- # workaround: anthropics/claude-code#13003
depends:
    - Skill(llm-design-kb)
---

# Technical Policy — architecture design rules

Cross-cutting normative constraints (means, not ends) for the template's
architecture — bukzor's non-negotiables and strong preferences, made explicit.

Each policy carries:

- `force:` — RFC 2119 requirement level (`must` / `should` / `may`); schema in
  `technical-policy.jsonschema.yaml`. `must` = non-negotiable, `should` =
  strong, `may` = preference.
- `why:` — the goal in `../design/020-goals.kb/` (or the mission) it serves.

A policy may be broader than this template's mission — a universal engineering
principle that binds the template _a fortiori_. Breadth is not a disqualifier: a
constraint wider than the scope still governs the scope. Such a policy's `why:`
names the goal it most serves here, even when the principle reaches further.

The body states the rule normatively. The _descriptive_ justification (why the
rule is correct/effective) lives in `/discourse.kb/` and is cited inline — this
is the normative side of that boundary.
