# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Personal website for Daniel Dewar, hosted at pcdkd.xyz. Built with Hugo and deployed via GitHub Pages (CNAME file configures the custom domain).

## Build & Dev Commands

- **Local dev server:** `hugo server`
- **Build:** `hugo` (outputs to `public/`)

## Architecture

This is a minimal Hugo site with no theme — the entire site is a single page rendered by `layouts/index.html`. The HTML includes inline CSS (Emotion-style class names from an earlier Next.js build that was converted to static HTML).

Key files:
- `config.toml` — Hugo config (base URL, title, disabled taxonomy kinds)
- `layouts/index.html` — The complete single-page site (HTML + inline CSS)
- `static/` — Static assets (favicon, `.well-known/nostr.json`)
- `CNAME` — GitHub Pages custom domain (`pcdkd.xyz`)
