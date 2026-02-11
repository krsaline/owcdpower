# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static website for the Ocotillo Water Conservation District (OWCD) — an Arizona public power utility serving southern Maricopa County (Chandler area). The site provides rate information, solar/DG interconnection resources, customer enrollment, outage reporting, and public documents.

## Architecture

This is a zero-build static site. There is no bundler, framework, package manager, or build step. To develop, open the HTML files directly in a browser.

### Files

- **`index.html`** — Simpler wireframe/template version with placeholder content and a civic blue/desert copper palette. Uses minimal JS (parallax effect, copyright year).
- **`owcd.html`** — Full-featured production page with a water-blue/turf-green palette inspired by the Ocotillo Golf Course. Includes:
  - Hero image slideshow (4 slides, auto-advance)
  - Leaflet.js interactive map of the district (CDN-loaded)
  - Bill estimator calculator (residential overhead/underground, commercial)
  - Scroll-reveal animations via IntersectionObserver
  - Google Fonts (Playfair Display + Outfit)

### Key Patterns

- All CSS is inline within `<style>` tags — there are no external stylesheets.
- All JS is inline within `<script>` tags at the bottom of the page — there are no external JS files.
- Both files use CSS custom properties (`:root` variables) for theming. The two files have entirely different color palettes.
- External dependencies are CDN-loaded only: Leaflet 1.9.4, Google Fonts. No local vendor files.
- Hero slideshow images in `owcd.html` are served from `static/images/` (local). Background images in `index.html` still reference Unsplash CDN URLs.
- Rate data (effective May 1, 2024) is hardcoded in both the HTML display and the JS calculator in `owcd.html`. When rates change, update both the rate cards and the `R` object inside `calcBill()`.
- Tax rate (9.05% combined: 5.6% AZ + 0.7% Maricopa + 2.75% Chandler) is hardcoded in the calculator.

### Responsive Behavior

Both files collapse to single-column layouts at `max-width: 900px` (index) / `920px` (owcd). Navigation links hide at mobile breakpoints — no hamburger menu is implemented yet.
