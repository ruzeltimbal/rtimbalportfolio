# CLAUDE.md

Guidance for Claude Code when working in this repository.

## What this is

A single-page personal portfolio site for **Ruzel P. Timbal** (Data & Reporting Analyst).
It is a **static site** — plain HTML, CSS, and vanilla JavaScript with **no build step, no
dependencies, and no framework**. Everything ships as-is to the browser.

- **Live URL:** https://ruzeltimbal.github.io/rtimbalportfolio/
- **Host:** GitHub Pages, served from the `main` branch of `ruzeltimbal/rtimbalportfolio`.
- **Deploy:** pushing to `main` publishes the site. There is nothing to build or bundle.

## Key files

| File | Purpose |
| --- | --- |
| `index.html` | The entire site — HTML, all CSS (in one `<style>` block), and all JS (in one `<script>` block at the bottom). This is where ~all edits happen. |
| `resume-src.html` | Print-oriented HTML source for the résumé (A4 `@page`, its own styles). Used to generate the résumé PDF. |
| `Ruzel-Timbal-Resume.pdf` | The downloadable résumé linked from the site (hero + contact section). |
| `sitemap.xml`, `robots.txt` | SEO. Update `<lastmod>` in `sitemap.xml` on significant content changes. |
| `googlee20d5549bfd0b60c.html` | Google Search Console verification token — do not delete. |
| `favicon-*.png`, `apple-touch-icon.png` | Icons referenced from `<head>` in `index.html`. |
| `og-banner.png` | Social/link-preview image referenced by Open Graph / Twitter meta tags. |
| `photo.png` | Hero avatar. |

Files ignored by git (local-only, see `.gitignore`): `Screenshot*.png`,
`2604 Ruzel P. Timbal Resume.pdf`, `*.url`.

## How the page is structured

`index.html` is a flat sequence of `<section>` blocks in this order: nav → hero → stats →
about → skills → experience (timeline) → projects → education → contact → footer.
Section styling is driven by CSS custom properties defined in `:root` (colors like
`--navy`, `--accent`, spacing like `--radius`). **Reuse these variables** rather than
hardcoding hex values so the palette stays consistent.

The JS at the bottom of `index.html` does four things, all vanilla + `IntersectionObserver`:
1. Sets the footer year.
2. Assembles the contact email at runtime (anti-scraper — the address is split into
   `user`/`domain` vars and never appears literally in the HTML source). Keep this pattern
   if you touch the email.
3. Reveal-on-scroll animations (`.reveal` → `.in`) and animated skill bars (`data-w`).
4. Chart build animations for project cards (`.proj-viz` → `.play`) and count-up stats.

All animations honor `prefers-reduced-motion` — preserve that when adding motion.

## Conventions

- **Everything is inline** in `index.html` (single-file site). Don't split CSS/JS into
  separate files unless the user asks — it would change the deploy shape for no benefit.
- Match the existing style: 2-space indentation, CSS grouped by section with comment
  banners, semantic HTML, accessibility attributes (`aria-hidden`, `alt`, width/height on
  images).
- Content (job history, skills, projects) exists in **two places**: the site
  (`index.html`) and the résumé (`resume-src.html` / the PDF). When updating facts like
  dates, titles, or contact info, check whether both need the change.

## Verifying changes

No test suite. To check work, open `index.html` in a browser (or use a local static
server) and visually confirm layout, links, and animations. Check responsive behavior —
there are mobile breakpoints at 640/720/820px.

## Git

- Default branch is `main`; commits to it deploy the live site, so treat `main` as
  production. Confirm content/factual changes with the user before committing.
- Commit messages in this repo are short and descriptive (e.g. "Add data-themed UI
  animations", "Add sitemap.xml and robots.txt for search engines").
