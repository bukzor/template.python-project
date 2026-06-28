---
kind: article
title:
  "Buck2 OSS third-party state (Stumbling through Buck2; issue #132; no-prelude
  intro)"
authors: [Eric Zhang, facebook/buck2 community]
url: https://gist.github.com/ekzhang/fcfa8cf1df4257cc51c02d5ddc4fe46b
likelihood: 0.85
tags: [buck2, third-party, python, node, pnpm, maturity]
---

# Buck2 OSS third-party roughness

Community evidence that the open-source third-party-dependency story is uneven:
**cargo** is paved (reindeer), **python/uv** is DIY (no first-class importer;
uv's lockfile is conceptually ideal but unbridged), **npm/pnpm** is the roughest
(prelude has internal js/node rules used at Meta, but no documented OSS pnpm
third-party flow; no bzlmod-equivalent). See also facebook/buck2 issue #132.
Reliability < 1.0 because it is community testimony on a fast-moving target.
