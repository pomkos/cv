# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A Jekyll site that renders Peter Gates' CV (`index.md`) and resume (`resume.md`) as static HTML, published via GitHub Pages at https://pomkos.github.io/cv.

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
