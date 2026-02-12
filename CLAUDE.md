# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Hugo static site for [marek.onl](https://marek.onl) — a personal notes blog. Uses the Statine theme (git submodule at `themes/statine/`, repo: `gitlab.com/upbqdn/statine`).

## Commands

Build and serve locally:
```
hugo server
```

Build for production:
```
hugo
```

Rebuild Tailwind CSS (run from theme directory after editing `themes/statine/assets/css/main.css`):
```
cd themes/statine && npm run build-tw
```

Generate Pagefind search index (run after `hugo` build):
```
pagefind --site public
```

## Architecture

- `config.toml` — Site config: base URL, taxonomies (tags only), permalink rules, MathJax, unsafe HTML enabled
- `content/` — Markdown posts with TOML front matter (`+++`). Gitignored (content managed separately)
- `static/` — Favicons, data files (charts, mining media). `_pagefind/` and `data/` are gitignored
- `themes/statine/` — Git submodule; has its own `CLAUDE.md` with detailed theme architecture

The theme handles: Tailwind CSS v4 pipeline, dark mode (system `prefers-color-scheme`), MathJax, Pagefind search UI, Remark42 comments, EB Garamond + Iosevka fonts, Schema.org microdata.

## Content Format

Posts use TOML front matter:
```toml
+++
title = "Title"
author = ["Marek"]
date = 2023-08-06T19:19:00+02:00
lastmod = 2023-12-01T22:08:00+01:00
tags = ["math", "definitions"]
draft = false
+++
```

Internal cross-references use `{{< relref "file.md" >}}`. Math uses LaTeX via MathJax (`\(...\)` inline, `$$...$$` display).
