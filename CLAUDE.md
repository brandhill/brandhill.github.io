# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single-page personal portfolio website served at **brandhill.github.io** (GitHub Pages, user site). It is built on the Start Bootstrap "Creative" theme (Bootstrap 3, jQuery) and is entirely static — there is **no build system, package manager, test suite, or CI**. The published site is the repository root served verbatim.

## Develop / preview / deploy

- **Preview:** open `index.html` directly in a browser, or serve the root statically (e.g. `python3 -m http.server`).
- **Deploy:** push to the `master` branch. GitHub Pages serves the repo root — there is no build step, so a commit to `master` *is* the deploy.
- There is nothing to lint, build, or test.

## Architecture

All page content lives in `index.html` as a single scrolling page with anchored sections: `#about`, `#skill`, `#portfolio`, `#contact`. Navigation uses Bootstrap scrollspy/affix plus jQuery Easing smooth-scroll wired up in `js/creative.js`.

**Portfolio items are hardcoded HTML blocks.** Each project is a `<div class="col-lg-4 col-sm-6">` containing an `<a class="portfolio-box">` with an `<img>` from `img/` and a caption (`.project-name` / `.project-category`). To add/edit a project, duplicate one of these blocks in the `#portfolio` section — there is no data file or templating.

**Styling:** `css/creative.css` is the single source of truth — edit it directly. (The original LESS source under `less/` was removed because it had drifted out of sync with the compiled CSS and there was no build step to reconcile them.) Theme colors are `#F05F40` (primary accent) and `#222` (dark), repeated literally throughout `creative.css`.

**Vendored third-party assets** (do not hand-edit): `css/bootstrap*.css`, `css/animate.min.css`, everything under `font-awesome/`, and the `js/` libraries (jQuery, Bootstrap, WOW.js, FitText, easing). `js/creative.js` and `css/creative.css` carry the Start Bootstrap header but hold this site's custom behavior/styles.

## Notes / gotchas

- `index.html` loads Google Fonts from `https://fonts.googleapis.com` (with `preconnect`). There is no analytics on the page.
- Images live in `img/`; full-resolution originals are kept under `img/original/`. Served images are intentionally compressed/resized (see git history) — keep the served copies optimized.
- Per global git policy, commit messages must **not** include a `Co-Authored-By` line.
