# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

Personal portfolio site for Oluwasijibomi Solola (siji.dev). Pure vanilla HTML/CSS/JS — no build step, no package manager, no framework, no test suite.

## Development

Open `index.html` directly in a browser. There are no build, lint, or test commands.

For live-reload during development, use a local server (e.g. VS Code Live Server extension or `npx serve .`).

## Architecture

Three files do all the work:

- **[index.html](index.html)** — all page content and structure
- **[style.css](style.css)** — all styling, including theme tokens
- **[index.js](index.js)** — theme toggle and scroll-reveal logic only

### Theme system

CSS custom properties are defined on `[data-theme="dark"]` and `[data-theme="light"]` selectors at the top of [style.css](style.css). Every colour in the file references a variable (e.g. `var(--teal)`, `var(--amber)`, `var(--bg)`). `index.js` toggles the `data-theme` attribute on `<html>` and persists the choice to `localStorage`.

### Scroll-reveal

Elements with class `reveal` start at `opacity: 0; transform: translateY(28px)`. An `IntersectionObserver` in [index.js](index.js) adds class `visible` when they enter the viewport, triggering the CSS transition. Stagger delays are applied via `.stagger .reveal:nth-child(n)` selectors in CSS.

### Content note

[index.md](index.md) is an older draft of the page content and is **out of sync** with [index.html](index.html) — it lists different projects and metrics. Treat [index.html](index.html) as the source of truth. The `.md` file is not rendered anywhere.

## Design conventions

- **Fonts**: Playfair Display (headings, serif), DM Mono (labels, badges, code-style), Outfit (body)
- **Accent colours**: teal (`--teal`) for primary actions and n8n content; amber (`--amber`) for UiPath/RPA content
- **Card variants**: `.pcard` for n8n project cards, `.ucard` for UiPath cards; `.wide.flagship` spans full grid width
- **Responsive breakpoint**: single breakpoint at `860px` — nav links hide, multi-column grids collapse to 1 column
