# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this project is

A static HTML study guide for the **HCIC** (robotics/industrial computing competition) consisting of five standalone HTML files served via `index.html`. No build system, no dependencies to install, no server required — open `index.html` in a browser.

## File layout

| File | Role |
|------|------|
| `index.html` | Shell: left nav, topbar, iframe container, progress tracking, keyboard shortcuts |
| `Chapter1_Mechanical_and_Robot_Structure.html` | Standalone chapter page |
| `Chapter2_Gear_Transmission_Calculations.html` | Standalone chapter page |
| `Chapter3_Sensors_and_Robot_Control.html` | Standalone chapter page |
| `Chapter4_Robot_Motion_Algorithms.html` | Standalone chapter page |
| `Formula_Quick_Reference_Card.html` | Formula reference page |

## Architecture

`index.html` is a shell that loads chapter files into an `<iframe id="content-frame">`. Each chapter HTML file is fully self-contained (its own `<style>`, MathJax CDN script, and content) so it renders correctly both inside the iframe and when opened directly.

**Styling conventions shared across all files:**
- Dark theme using CSS custom properties (`--bg`, `--surface`, `--border`, `--accent1`…`--accent5`, `--text`, `--text-muted`, `--heading`)
- Font stack: `Nunito` (body) + `JetBrains Mono` (code) from Google Fonts CDN
- LaTeX math rendered by MathJax 3 (`tex-svg`) loaded from jsDelivr CDN — inline math uses `$…$` or `\(…\)`, display math uses `$$…$$` or `\[…\]`

**Navigation state** in `index.html` is managed entirely in vanilla JS: `loadPage(idx)` sets the active nav item, loads the iframe src, marks chapters as visited, and updates the progress bar. Keyboard shortcuts: `←/↑` previous, `→/↓` next, `B` toggles sidebar.

## Editing guidelines

- When adding or modifying content in a chapter file, keep the CSS variables consistent with the existing palette; do not introduce new colour names.
- Each chapter page is intentionally independent — do not add imports or shared JS between chapter files and `index.html`.
- MathJax is loaded from CDN; no local copy exists. Formulas must follow standard LaTeX syntax compatible with MathJax 3.
- To add a new chapter: create a new standalone HTML file following the existing chapter template, then add a matching `<div class="nav-item">` entry in `index.html` and a welcome card in `#welcome`.
