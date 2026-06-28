---
kind: authority
title: "Reindeer — transform Cargo dependencies into generated Buck build rules"
authors: [facebookincubator]
url: https://github.com/facebookincubator/reindeer
tags: [buck2, cargo, rust, third-party, buckify]
---

# Reindeer

First-party Meta tool that reads `Cargo.toml`/`Cargo.lock`, vendors crates, and
**generates** BUCK rules for third-party Rust dependencies (`fixups.toml` for
`build.rs` crates). Buck2 builds _itself_ this way. The canonical proof that
"native manifest in → BUCK out" works for third-party, and the maturity bar the
Python/Node importers do not yet meet.
