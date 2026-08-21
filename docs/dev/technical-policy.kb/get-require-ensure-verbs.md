---
force: should
why:
  - design/020-goals.kb/uniform-polyglot-model.md
---

# CI scripts use get- / require- / ensure- verbs

The portable scripts **should** present exactly three public verb prefixes, each
with a fixed contract:

- `get-<noun>` — pure read; prints exactly one value to stdout (diagnostics to
  stderr), or errors. No effects.
- `require-<condition>` — pure assertion; the exit status _is_ the answer. No
  effects.
- `ensure-<state>` — idempotent converge: already-so → no-op; not-so → minimal
  act; conflicting/impossible → error. The only public verb with effects.

There **should** be no `do-` prefix: it is a type-name that earns nothing, since
`ensure-` already names the idempotent contract. Bare imperatives (`build`,
`publish`) survive only as **private** one-shot mechanisms beneath an `ensure-`,
never in the public surface.

The failure half of each contract is mandatory, not stylistic — see
`wrong-is-loud-or-impossible.md`. Single-responsibility verbs are what let one
small set compose into any workflow shape while keeping each guard local and
total.
