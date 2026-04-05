# CLAUDE.md — EZ Buses

This file tells Claude Code how this project is structured and how to work with it.

## Project Overview

Single-page static website for **EZ Buses** (ezbuses.ca) — a Toronto-area charter bus company. The entire site lives in one file: `index.html`. No build step, no dependencies, no frameworks.

## File Map

| File | Purpose |
|------|---------|
| `index.html` | Complete site — all HTML, CSS, and JS inline |
| `robots.txt` | Allows AI crawlers (GPTBot, Claude-Web, Perplexity, etc.) |
| `llms.txt` | Structured markdown for AI agents describing services and areas |
| `README.md` | Setup, deployment, and usage docs |

## How to Run Locally

```bash
python3 -m http.server 3000
# or
npx serve .
```

Open [http://localhost:3000](http://localhost:3000).

## Making Changes

All edits happen in `index.html`. The file is structured as:

1. `<head>` — meta tags, fonts, Schema.org JSON-LD
2. `<style>` — all CSS (scoped with descriptive class names)
3. `<body>` — page sections in order: hero → answer box → track record → services → map → FAQ → quick facts → quote form
4. `<script>` — FAQ accordion toggle and form honeypot logic

### Common tasks

- **Change phone/email** — search for `416-438-7371` or `ezbuses@gmail.com`
- **Update stats** — search for `15,000` (trip count) or `20+` (years in business)
- **Edit services** — look for the `<section id="services">` block
- **Update areas served** — SVG map is inside `<section id="areas">`, city list is in a `<ul>` below the SVG
- **Edit FAQ** — look for `<section id="faq">`, each item is a `<details>` element
- **Change colors** — CSS variables are at the top of the `<style>` block under `:root`
- **Change fonts** — Google Fonts `<link>` is in `<head>`, font-family declarations are in `:root`

## Deployment

Netlify auto-deploys on every push to `main`. No build command needed — publish directory is `.`.

To deploy a change:

```bash
git add index.html
git commit -m "your change description"
git push
```

Netlify picks it up within ~30 seconds.

## Form Submissions

The quote form uses Netlify Forms. Submissions go to the Netlify dashboard under **Forms > quote** and can be forwarded to an email via **Forms > Notifications**. Do not rename the `name="quote"` attribute on the `<form>` tag — Netlify uses it to identify the form.

## Brand Guidelines

- **Primary color:** `#1a1a2e` (dark navy)
- **Accent color:** `#e8c84a` (gold/yellow)
- **Display font:** Syne
- **Body font:** Urbanist
- **Tone:** Professional, trustworthy, GTA-local

## What NOT to do

- Do not add a build step or package.json — the site is intentionally dependency-free
- Do not replace the inline SVG map with a Google Maps embed — no API key needed this way
- Do not rename the Netlify form (`name="quote"`) without updating Netlify settings
- Do not remove `llms.txt` or `robots.txt` — they are part of the AI SEO strategy
