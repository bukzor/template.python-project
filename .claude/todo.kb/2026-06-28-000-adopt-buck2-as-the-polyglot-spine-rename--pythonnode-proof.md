---
managed-by: Skill(llm-subtask)
status: open
cost-benefit-sweh:
  timebox:
    "@value": 12
    rationale:
      rename + two-toolchain buckify + cell-alias spike + third-party derisk;
      high complexity, reassess after the spike
    confidence: tentative
  benefit-2w:
    "@value": 1
    rationale:
      strategic bet; unification value is long-horizon, little realized within
      2w
    confidence: tentative
  cost-of-delay-2w:
    "@value": 0.2
    rationale:
      design fully recorded in discourse.kb + design tower; decay limited to
      unrecorded nuance
    confidence: unsure
---

# Adopt buck2 as the polyglot spine: rename + Python+Node proof

**Priority:** Medium **Complexity:** High **Context:** The repo-specific
next-actions from the 2026-06-24/25 design conversation. Full reasoning of
record: `discourse.kb/` (descriptive) and `docs/dev/design/` +
`docs/dev/technical-policy.kb/` (normative). Session background:
`~/.claude/sessions.kb/template-polyglot-monorepo-architecture.md`. Do not
re-litigate the decisions there — extract and execute.

## Problem Statement

The template's settled direction is a polyglot, self-similar, composable repo
template with **buck2 as the cross-ecosystem unifying spine** and native tools
(uv/pnpm/cargo) as the drive-by surface. None of it is built yet. buck's
_unification_ value only shows at 2+ ecosystems, so the first concrete proof
must be two-language.

## Implementation Steps

- [ ] **Rename the repo** — "python-project" is already false (it ships
      `package.json`/pnpm/prettier). Pick a polyglot name; update copier config,
      remotes, references.
- [ ] **Buckify this repo as a Python+Node two-language proof**
  - [ ] `.buckconfig` with `[external_cells] prelude = bundled`
  - [ ] a Python toolchain + a Node toolchain
  - [ ] `apps/ lib/ packages/` expressed as uniform BUCK files
  - [ ] native manifests preserved underneath as per-package leaves + the
        drive-by build (buck behind native tools)
- [ ] **Cell-alias spike** — a two-repo toy proving a leaf builds both
      standalone and composed under a generated super-root. **Gates the
      compose-on-demand bet**
      (`discourse.kb/claims.kb/compose-on-demand-generated-view.md`); do this
      before betting the architecture on it.
- [ ] **Derisk third-party buckify for Python/pnpm** — cargo is paved
      (reindeer); python is DIY; pnpm is roughest. The open maturity risk
      (`discourse.kb/claims.kb/third-party-importers-remain-per-ecosystem.md`).

## Open Questions

- [ ] Order: rename first (cheap clarity) or prove buck first (de-risk the
      thesis)?
- [ ] Does the Node proof reuse the existing `package.json`/pnpm setup as-is?

## Success Criteria

- [ ] `buck build //...` builds both a Python and a Node target in one graph.
- [ ] A drive-by contributor can still build/test via native tools alone.
- [ ] The cell-alias spike builds a leaf standalone AND composed.

## Notes

Related, tracked separately: the `project_type: app|lib` question is reframed by
this direction as "where the primary package lands" (`apps/{slug}` vs
`packages/pypi/{slug}`) — see
`2026-06-24-000-copier-projecttype-app--lib-question.md`.

The personal-global _hoist_ of the convention + values is a different scope,
queued at `~/.claude/todo.kb/2026-06-27-000-hoist-…` (candidate home
`private.bukzor-llc`) — not part of this repo todo.
