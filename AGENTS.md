# AGENTS.md — ASX AI Structural Comparison

Static HTML site deployed on Netlify. No build step, no framework. Each file is a self-contained HTML document with embedded CSS and JavaScript.

## What this is

IMPACT × FAVES dual-axis analysis of AI executive job exposure across 5 ASX-listed companies. 599 tasks, 51 executives, 5 constraint archetypes. Built and iterated by Walter Adamson (OutcomesNow).

## File map

| File | Route | Purpose |
|------|-------|---------|
| `asx_ai_exposure_portfolio_contrast_map.html` | `/` | Homepage — contrast map, landing page, reading order |
| `how_to_read_these_dashboards.html` | `/guide` | Framework explainer (IMPACT, FAVES, quadrants, constraints) |
| `impact_x_faves_5company_asx_portfolio_synthesis.html` | `/portfolio` | Capstone synthesis — cross-company charts, CFO signals, board questions |
| `genusplus_gnp_ai_job_exposure_dashboard.html` | `/genusplus` | GenusPlus (GNP) — Atoms constraint |
| `wisetech_wtc_ai_job_exposure_dashboard.html` | `/wisetech` | WiseTech Global (WTC) — Bits constraint |
| `kellypartners_kpg_ai_job_exposure_dashboard.html` | `/kellypartners` | Kelly Partners (KPG) — Institutional constraint |
| `csl_csl_ai_job_exposure_dashboard.html` | `/csl` | CSL Limited (CSL) — Atoms + Institutional constraint |
| `seek_sek_ai_job_exposure_dashboard.html` | `/seek` | SEEK Limited (SEK) — Cognitive constraint |
| `genusplus_gnp_ai_instinct_assessment.html` | `/genusplus-instinct` | Earlier-format GenusPlus assessment (different lens) |

## Design system

All files share a consistent design system defined inline in each file's `<style>` block. CSS custom properties:

```css
--ivory: #f5f4f0     /* page background */
--white: #ffffff     /* card background */
--charcoal: #1a1a1a  /* primary text */
--noir: #0a0a0a      /* site nav background */
--stone: #8a8680     /* secondary/muted text */
--border: #d8d4cc    /* card/divider borders */
--accent: #1d4ed8    /* blue — links, highlights */
--green: #16a34a     /* Automate quadrant */
--orange: #d97706    /* Augment quadrant */
--purple: #6366f1    /* Converge quadrant */
--slate: #64748b     /* Hold Fast quadrant */
```

Typography: `Instrument Serif` (headings), `DM Sans` (body), `JetBrains Mono` (code/labels). All loaded from Google Fonts.

## Charts (Chart.js)

Charts use `maintainAspectRatio: true` with explicit `aspectRatio` values — not fixed pixel heights. Ratios by chart type:
- Radar: `1` (square)
- Scatter/bubble: `1.2–1.3`
- Bar: `2–2.2`

This makes charts responsive without media query overrides. Do not reintroduce fixed `height` or `canvas` height attributes.

## Site navigation

Each page includes a shared `.site-nav` bar (inline `<style>` + `<nav>` block, black background `#0a0a0a`). The nav links to `/`, `/guide`, `/portfolio`, and all five company dashboards. When adding a new page, add a nav link to all existing files.

## Deployment

Netlify. `netlify.toml` maps clean URLs to verbose filenames (e.g. `/seek` → `seek_sek_ai_job_exposure_dashboard.html`). No build command — `publish = "."`. When adding a new HTML file, add a corresponding redirect in `netlify.toml`.

## Conventions

- **Filenames**: `{company}_{ticker}_{type}.html` — lowercase, underscores
- **Commit messages**: conventional commits — `feat`, `fix`, `docs` with scope in parens, e.g. `fix(charts): ...`
- **No Xero**: XRO was planned but not analysed — do not add placeholder content for it
- **Self-contained files**: CSS, JS, and data all inline — no external `.js` or `.css` files
- **Co-authorship**: commits include `Co-Authored-By: Oz <oz-agent@warp.dev>` when Oz assisted

## Adding a new company dashboard

1. Copy an existing dashboard (e.g. `seek_sek_ai_job_exposure_dashboard.html`) as a template
2. Name it `{company}_{ticker}_ai_job_exposure_dashboard.html`
3. Update the site nav in all existing files to include the new page
4. Add a redirect in `netlify.toml`
5. Update `README.md` portfolio table
