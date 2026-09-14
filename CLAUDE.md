# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A Jekyll site that renders Peter Gates' CV (`index.md`) and resume (`resume.md`) as static HTML, published via GitHub Pages at https://pomkos.github.io/cv.

## IMPORTANT: `master` is not the live site

GitHub Pages for this repo is configured to build from the **`gh-pages` branch**, not `master`. The two branches have diverged and hold genuinely different content (`gh-pages`'s `index.md` has its own tagline, contact links, and some sections that are further ahead than `master`'s, e.g. newer publications) — `gh-pages` has no `resume.md` or `CLAUDE.md` at all, only `index.md` plus the same layout/media/config files.

Editing `master` alone does **not** update the live site. Any content change meant to reach https://pomkos.github.io/cv must also be made on `gh-pages` (`git checkout gh-pages`, edit `index.md` there, commit, push) — check the existing `gh-pages` copy first rather than assuming it matches `master`, since the two have been maintained somewhat independently. Confirm with the user before merging the branches outright, since `gh-pages` carries content differences that may be intentional.

## Running locally

```
./start_cv.sh
```

This runs `jekyll serve -P 3232 -H 0.0.0.0 -B` from `~/projects/cv` (a hardcoded path from the original author's machine — `cd` there manually or run the `jekyll serve` command directly from this repo's root if that path doesn't exist on your machine). Requires Jekyll/Ruby installed locally; there is no `Gemfile` in the repo, so dependencies are whatever's globally available.

There are no build scripts, linters, or tests in this repo — it's rendered entirely through GitHub Pages' built-in Jekyll pipeline.

## Structure

- `index.md` / `resume.md` — the two content pages, both using `layout: cv`. They contain near-duplicate content (index.md is the fuller CV, resume.md is a condensed version) — when updating shared facts (education, positions, publications), check whether the change applies to both files.
- `_layouts/cv.html` — the single layout wrapping page content in `<div id="main"><div id="content">`, and pulling in a stylesheet pair (`{{ site.style }}-screen.css` / `-print.css`) from `media/`.
- `_config.yml` — sets `style: davewhipp` (alternative: `kjhealy`), selecting which stylesheet pair in `media/` is used, and `markdown: kramdown`.
- `media/` — two complete CSS theme pairs (screen + print stylesheets) for davewhipp and kjhealy; switching themes is a one-line change in `_config.yml`, not a CSS edit.
