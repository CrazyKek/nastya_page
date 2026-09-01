# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

A static personal/CV website for Anastasia Chebotareva. No build system, no dependencies — pure HTML, CSS, and vanilla JS. Deployed on Railway via Caddy serving static files.

## Structure

```
index.html          — main CV/landing page
portfolio/
  index.html        — copywriting portfolio page
styles.css          — shared design system (imported by both pages)
```

## Running locally

Open either HTML file directly in a browser — no server required. To test with a local HTTP server:

```bash
python3 -m http.server 8000
```

## Design system

All design tokens live in `styles.css` as CSS custom properties on `:root`. Dark mode is handled via `@media (prefers-color-scheme: dark)` — no JS theme switching.

**Fonts** (loaded from Google Fonts):
- `Instrument Serif` — display headings on the main page only
- `Source Sans 3` — body text and headings on the portfolio page

**Key tokens:** `--bg`, `--surface`, `--text`, `--muted`, `--link`, `--border-accent`, `--accent`

**Card pattern:** left border (`3px solid var(--border-accent)`) + `var(--surface)` background + `border-radius: 0 4px 4px 0`. Used for `.aside-card`, `.contact-card`, and `.callout`.

**Section animations:** `.section` elements start `opacity: 0; transform: translateY(12px)` and transition to `.visible` via an `IntersectionObserver` (threshold 0.15) defined inline at the bottom of each HTML file. Hero/intro cards use CSS `@keyframes fadeInUp` instead (no JS needed for above-the-fold elements).

## Page-specific styles

Both pages share `styles.css` for base reset, tokens, container, links, list styles, and animation classes. Each page then has a `<style>` block in `<head>` for its own component styles. Keep shared rules in `styles.css`; keep page-specific rules inline.

## Content language

Page content is in Russian. Keep all user-facing text in Russian unless the user specifies otherwise.
