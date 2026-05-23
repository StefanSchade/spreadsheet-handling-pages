# reveal.js 4.6.1 — vendored bundle

This directory contains an unmodified copy of [reveal.js](https://revealjs.com)
version 4.6.1, vendored into the `spreadsheet-handling-pages` site as the
runtime asset for the demo walkthrough slide decks under
`versions/<tag>/demo/slides/` and `latest/demo/slides/`.

## Why vendored

Earlier slide builds loaded reveal.js from a public CDN
(`cdn.jsdelivr.net/npm/reveal.js@4`). Vendoring a pinned version:

* makes published slides reproducible — they do not depend on the CDN
  serving a specific point release;
* satisfies the MIT attribution requirement cleanly: the `LICENSE` file
  ships next to the distributed code;
* removes the build-time dependency on CDN availability.

## Contents

* `dist/`     — the reveal.js production bundle (CSS + JS + themes).
* `plugin/`   — the official plugin set bundled with reveal.js
  (highlight, markdown, math, notes, search, zoom).
* `LICENSE`   — the original MIT license from reveal.js 4.6.1.
* `REVEALJS-README.md` — the original reveal.js README for reference.

## Bumping the pinned version

To move to a newer reveal.js 4.x or 5.x:

. Pick the new version (e.g. `4.6.2`).
. Run `npm pack reveal.js@<version>` and extract into a fresh sibling
  directory `assets/reveal.js@<version>/`.
. Update `demo/scripts/render_slides.sh` and the demo publish workflow to
  point `REVEALJS_DIR` (and the slide href base) at the new directory.
. Verify a rendered deck loads in a browser before tagging a release.
. Once the new directory has shipped in at least one release, the old
  pinned bundle can be removed.

Keeping older pinned bundles alongside the newest lets old
`versions/<tag>/demo/slides/` snapshots continue to load their matching
reveal.js without retroactive edits.
