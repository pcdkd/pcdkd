# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Personal website for Daniel Dewar, hosted at pcdkd.fyi on Netlify (CNAME holds the custom domain). Plain static HTML, no framework. The Hugo files (`config.toml`, `archetypes/`, `content/`, `public/`) are leftovers from an earlier build and are not used.

## Build & Dev Commands

- **Build:** the command in `netlify.toml` copies `layouts/index.html` and `static/` assets into `dist/`.
- **Local preview:** run that copy step, then `cd dist && python3 -m http.server 8765` and open http://localhost:8765/.

## Architecture

The entire site is a single page in `layouts/index.html` (HTML, inline CSS, and one inline script). The background is a pixel-art canvas of the Brooklyn Bridge and Manhattan from DUMBO, colour-graded live:

- **Time of day and season:** the sun's elevation for DUMBO is computed in the browser (NOAA solar equations) and drives a palette keyed by elevation, with separate morning and evening tables. Sunset therefore moves with the calendar and winter middays stay lower and warmer.
- **Weather:** fetched from Open-Meteo (no API key) for DUMBO on load, cached in localStorage for 10 minutes, refreshed every 15. Cloud cover desaturates and dims the grade, fog is a banded overlay over distant Manhattan, rain and snow are particle layers, thunder adds occasional flashes, and wind speeds up the East River water and pushes precipitation sideways.
- **Reduced motion:** water, particles, and flashes stop advancing when `prefers-reduced-motion` is set.

### Preview overrides (query string)

- `?at=YYYY-MM-DDTHH:MM` renders the scene at that New York wall-clock moment, e.g. `?at=2026-12-21T16:30`.
- `?wx=clear|cloudy|overcast|fog|drizzle|rain|snow|thunder` forces a weather state, optionally with `&wind=<km/h>`.

Key files:
- `layouts/index.html` — the complete single-page site
- `static/skyline.png` — the base pixel-art image the canvas grades
- `static/.well-known/nostr.json`, `static/favicon.ico` — copied verbatim into `dist/`
- `netlify.toml` — build command and publish directory
- `CNAME` — custom domain
