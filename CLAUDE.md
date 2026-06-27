# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single-page personal portfolio website served at **brandhill.github.io** (GitHub Pages, user site). It is built on the Start Bootstrap "Creative" theme (Bootstrap 3, jQuery) and is entirely static — there is **no build system, package manager, test suite, or CI**. The published site is the repository root served verbatim.

## Develop / preview / deploy

- **Preview:** open `index.html` directly in a browser, or serve the root statically (e.g. `python3 -m http.server`). A static server is preferred over `file://` because some referenced scripts (Respond.js) don't run under `file://`.
- **Deploy:** push to the `master` branch. GitHub Pages serves the repo root — there is no build step, so a commit to `master` *is* the deploy.
- There is nothing to lint, build, or test.

## Architecture

All page content lives in `index.html` as a single scrolling page with anchored sections: `#about`, `#skill`, `#portfolio`, `#contact`. Navigation uses Bootstrap scrollspy/affix plus jQuery Easing smooth-scroll wired up in `js/creative.js`.

**Portfolio items are hardcoded HTML blocks.** Each project is a `<div class="col-lg-4 col-sm-6">` containing an `<a class="portfolio-box">` with an `<img>` from `img/` and a caption (`.project-name` / `.project-category`). To add/edit a project, duplicate one of these blocks in the `#portfolio` section — there is no data file or templating.

**Styling has a source/compiled split that is not automated:**
- Source: `less/creative.less` (imports `less/variables.less` and `less/mixins.less`). Theme colors live in `variables.less` (`@theme-primary: #F05F40`, `@theme-dark: #222`).
- Compiled/served: `css/creative.css` — this is the file the browser actually loads.
- **No LESS compiler is committed.** Editing `.less` alone changes nothing on the live page. Either edit `css/creative.css` directly, or recompile with an external tool (`lessc less/creative.less css/creative.css`) and keep both in sync. Match whichever approach the surrounding commit history used.

**Vendored third-party assets** (do not hand-edit): `css/bootstrap*.css`, `css/animate.min.css`, `css/smart-app-banner.css`, everything under `font-awesome/`, and `js/` (jQuery, Bootstrap, WOW.js, FitText, easing). `js/creative.js` and `css/creative.css` carry the Start Bootstrap header but hold this site's custom behavior/styles.

## Notes / gotchas

- `index.html` loads Google Fonts over `http://` and has a Google Analytics (`UA-45269364-3`) snippet at the bottom of `<body>`.
- `css/smart-app-banner.css` is linked but no JS initializes a smart app banner — the stylesheet is present without active behavior.
- Images live in `img/`; full-resolution originals are kept under `img/original/`. Served images are intentionally compressed/resized (see git history) — keep the served copies optimized.
- Per global git policy, commit messages must **not** include a `Co-Authored-By` line.
