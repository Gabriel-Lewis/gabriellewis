# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A static, single-page personal portfolio site for Gabriel Lewis, served at gabriellewis.me. Built on the HTML5 UP **Strata** template (skel framework). All content lives in `index.html`; there is no backend, no framework, and no CMS.

## Deployment

Hosted on **GitHub Pages from the `gh-pages` branch** (the default/main branch of this repo). Pushing to `gh-pages` publishes the live site. `CNAME` maps the site to `gabriellewis.me` — do not delete it. There is no build/CI step: the files in the repo root are served as-is.

## Editing content

- Page content (Experience, Projects, Education sections) is hand-edited HTML in `index.html`. Sections use skel grid classes like `6u 12u$(xsmall)` — two columns that collapse to one on the `xsmall` breakpoint. Keep new `work-item` articles consistent with the existing markup.
- All work/company logos and thumbnails are local files in `images/thumbs/` (company logos are vendored simple-icons SVGs) — don't hotlink external images.
- The footer copyright year is injected by inline JS (`#year`); don't hardcode it.
- `sitemap.xml` `lastmod` timestamps are updated manually when content changes (see recent commit history).

## Styling — main.css and main.scss have diverged

`assets/css/main.css` was originally compiled from `assets/sass/main.scss`, but the two have diverged: the CSS has been hand-edited since 2017 (e.g. `.work-place-header` exists only in the CSS) while the SCSS went stale. **Do not recompile the SCSS over main.css — it would wipe those hand edits.** Until the SCSS is back-ported, treat `main.css` as the file that's actually served and apply any style change to *both* `main.css` and `main.scss` so they don't drift further.

The other CSS files (`font-awesome.min.css`, `brands.min.css`, `ie8.css`) are vendored and should not be edited. `font-awesome.min.css` is Font Awesome 6 with v4 shims; `brands.min.css` is *not* linked from `index.html` — brand glyphs missing from the shims (e.g. `.fa-bluesky`) get a `:before` rule at the bottom of `main.css`/`main.scss` instead.

## Structure notes

- `assets/js/` is vendored template JS (jQuery, skel, poptrox, util) plus the template's `main.js`. Site-specific behavior is minimal and lives inline in `index.html`. The poptrox lightbox is bound to `section#two` — keep that id even though the section is now titled "Projects".
- `favicons/` and `images/` hold static assets; `LICENSE.txt` is the template's CCA 3.0 license.
- Search-engine/Pinterest verification meta tags and the Google Analytics 4 (gtag.js) snippet are wired directly into `index.html`.