---
managed-by: Skill(llm-subtask)
cost-benefit-sweh:
  timebox:
    "@value": 2.0
    rationale: |
      One small script, one template change, and a five-repo
      propagation. Beyond two hours means `direnv exec` is fighting
      something -- stop and use the relative-path workaround, which is
      already proven.
  benefit-2w:
    "@value": 2.0
    rationale: |
      Every agent commit into an affected repo fails its hooks today.
      That is a daily tax with a confusing error message.
---

# `bin/direnv-exec` for entry points that need the `.envrc`

## The reproduction (found 2026-08-22)

`.pre-commit-config.yaml` in five repos declares `entry: pnpm-run` -- a bare
command name, resolvable only because `.envrc` puts `$REPO/bin` on `PATH`. Hooks
inherit the environment of the shell that ran `git commit`, and direnv loads
`.envrc` from an _interactive shell prompt in that directory_. Neither condition
holds for an agent:

```sh
$ (cd ~/repo/github.com/bukzor/typed-json && command -v pnpm-run)
# nothing: direnv never fired, because a non-interactive subshell has
# no prompt hook
```

That is why it did not reproduce by hand. `cd` into the repo in a terminal and
direnv activates, `PATH` gains `bin/`, the hook works. Agents commit with
`git -C <repo>` from a cwd in some _other_ repo -- `git -C` does not change
directories, so the target repo's `.envrc` is never a candidate for loading, and
`direnv revoke` on the current one changes nothing about that.

Affected: `basedpyright-as-pyright`, `bukzor.color`, `prototype.hearts-2025`,
`pyright-select`, `typed-json`. Already repaired: this repo and
`cros-claude-code-keepawake`, via `entry: bin/pnpm-run` -- a relative path,
which works because pre-commit runs hooks with cwd at the repo root.

## The work

The relative-path fix is proven and could be swept across the five today. It
repairs the lookup and nothing else: `bin/pnpm-run` still depends on `pnpm`
being globally installed, and any entry point that wants `.venv/bin` has the
same problem one layer down.

The general fix, per @bukzor: a `$REPO/bin/direnv-exec` that activates `.envrc`
whether or not the calling shell has it loaded -- `direnv exec "$REPO" "$@"` is
the primitive -- and every entry point that might need the environment goes
through it.

Order: write `bin/direnv-exec` here, move this repo's two hooks onto it, confirm
a `git -C` commit from outside passes, then propagate to the five.
