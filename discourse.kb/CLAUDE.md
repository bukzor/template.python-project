--- # workaround: anthropics/claude-code#13003
requires:
    - Skill(llm-discourse-graph)
---

# discourse.kb — template direction: polyglot, self-similar, buck-unified

Epistemic graph persisting the 2026-06 design conversation about what
`template.python-project` should become: a **polyglot, self-similar repo
template** with **buck2 as the cross-ecosystem unifying spine**, native package
managers (uv/pnpm/cargo) preserved as per-package leaves and the drive-by build
surface.

Entry point: `questions.kb/should-template-be-buckified.md` (the question the
conversation landed on) and `questions.kb/how-organize-polyglot-monorepo.md`
(the structural model).

Source of record: `sources.kb/design-chat-2026-06.md`.

## Descriptive here; normative next door

This graph holds the **descriptive** side of the conversation — _what's true,
what follows, what we concluded_. The **normative** side — _the values and
design rules_ (self-similar, drive-by-friendly, no-lockstep, …) that those
conclusions are _motivated by_ — lives in the design tower at
`/docs/dev/design/` (goals) and `/docs/dev/technical-policy.kb/` (the rules),
per `Skill(llm-design-kb)`. The policies there cite these claims as their
rationale. See `Skill(llm-discourse-graph)` → "Descriptive vs normative" for
when to reach across.
