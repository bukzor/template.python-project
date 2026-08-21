---
force: must
why:
  - design/020-goals.kb/uniform-polyglot-model.md
---

# Platform specifics isolated in providers/<name>/

Vendor and platform identifiers — `$GITHUB_*`, the `gh` CLI, OIDC ceremony,
registry hostnames — **must** appear only inside `lib/ci/providers/<name>/`
(e.g. `providers/github/`). Any such name **outside** that tree fails the build
(a `require-no-platform-leak` check). Core scripts consume only a provider's
normalized output (`get-context`, `get-check-status`, `get-creds`), never the
raw platform.

Providers are named for **what they represent** (`providers/github/`), never for
their type (not `adapters/`, not `utils/`) — you would not name a variable
`int`.

Only one provider exists today, and that is fine: it is a punt with a tripwire
(`punt-with-a-tripwire.md`). The named slot makes the second provider's arrival
obvious, and the no-leak check makes a hardcoded assumption that escapes the
slot fail loudly rather than quietly.

Non-negotiable: the moment a platform name leaks into the core, the
entry-point-agnostic core (`entry-point-agnostic-core.md`) is silently lost.
