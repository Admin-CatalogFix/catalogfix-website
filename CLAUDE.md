# CatalogFix Website

Single-page landing site for CatalogFix — expert-led Amazon and Walmart catalog support, not an agency.

## Project Files

```
catalogfix-website/
├── index.html        ← the site: HTML, CSS, and JS are all inline
├── 404.html          ← branded not-found page (GitHub Pages serves it automatically)
├── CNAME             ← custom domain for GitHub Pages (catalogfix.com)
├── robots.txt        ← allows all crawlers, points to sitemap
├── sitemap.xml       ← single-URL sitemap; update <lastmod> on content changes
├── assets/
│   ├── icon.png             ← nav icon mark, trimmed to content (458×247), displayed 44px tall
│   ├── logo.png             ← nav wordmark (490×130, cropped to content, displayed 30px tall)
│   ├── logo-src.png         ← original uncropped 500×500 wordmark
│   ├── favicon.png          ← 48×48, generated from icon-src.png
│   ├── apple-touch-icon.png ← 180×180, generated from icon-src.png
│   ├── icon-src.png         ← original 500×500 CF icon mark (source of truth for icon.png + favicons)
│   └── og-image.jpg         ← 1200×630 social share image
└── CLAUDE.md         ← this file
```

No build tools. No frameworks. No dependencies. Edit `index.html` directly and open it in a browser to preview.

To regenerate icons from the source mark (macOS):
```bash
sips -Z 48  -s format png assets/icon-src.png --out assets/favicon.png
cp assets/icon-src.png assets/apple-touch-icon.png && sips -Z 180 assets/apple-touch-icon.png
```

## Deployment

Hosted on GitHub Pages. Repo: [Admin-CatalogFix/catalogfix-website](https://github.com/Admin-CatalogFix/catalogfix-website) (public). Git credentials are stored in the macOS keychain.

To deploy changes:
```bash
git add -A
git commit -m "your message here"
git push
```

Custom domain: `catalogfix.com` (held in the `CNAME` file — don't delete it). DNS is managed at Squarespace and must point to GitHub Pages: A records on the apex to 185.199.108.153 / 185.199.109.153 / 185.199.110.153 / 185.199.111.153, and a `www` CNAME record to `admin-catalogfix.github.io`.

Note: `Admin-CatalogFix.io` is an older, stale repo from a previous attempt — the live site is this repo.

## Brand Colors

| Role | Hex |
|---|---|
| Charcoal Black (primary text) | `#111111` |
| Soft White (backgrounds) | `#F6F6F6` |
| Pure White | `#FFFFFF` |
| Dark Navy (hero, dark sections) | `#11283e` |
| Medium Navy (accents, eyebrows) | `#223f5a` |
| Primary Orange (CTAs, "Fix", highlights) | `#e88130` |
| Deep Orange (hover states) | `#d3671d` |

## Typography

- Font: **Inter** (loaded from Google Fonts) — fallback: Helvetica Neue, Arial
- Headings: `font-weight: 800`, tight `letter-spacing: -0.02em` to `-0.03em`
- Body: `font-weight: 400–500`, `line-height: 1.7–1.8`
- Eyebrows: `11–12px`, `font-weight: 700`, `letter-spacing: 0.12em`, `text-transform: uppercase`

## Page Sections (in order)

1. **Nav** — sticky, transparent over hero → solid dark navy on scroll. Logo is a horizontal lockup: `assets/icon.png` (CF mark) + `assets/logo.png` (wordmark), flex with `gap`. A `brightness(1.15)` filter lifts the navy ink on the dark bar. Mobile: full-screen hamburger overlay. Links: Services, How It Works, About, FAQ, Get in Touch.
2. **Hero** (`#home`) — dark navy bg, large headline, subhead, two CTA buttons, marketplace list
3. **Positioning** (`#what-we-do`) — "Not an agency" message + agency vs CatalogFix comparison table
4. **Services** (`#services`) — tabbed: Amazon (13 items) | Walmart (6 items). Soft white bg. Tabs are ARIA-compliant (role=tablist/tab/tabpanel, arrow-key navigation).
5. **How It Works** (`#how-it-works`) — dark navy bg, 3-step process (01/02/03)
6. **Values** (`#values`) — 2×2 grid of 4 values with SVG icons
7. **About** (`#about`) — origin story, left label + right long-form text, pull quote
8. **FAQ** (`#faq`) — 6 `<details>` accordions, white bg. **If FAQ copy changes, update the matching FAQPage JSON-LD in `<head>` too — they must stay in sync.**
9. **Contact** (`#contact`) — charcoal bg, email (JS-obfuscated), "what to expect" panel
10. **Footer** — near-black, logo text + tagline + copyright year (auto-updated via JS)

## SEO / Structured Data

- `<head>` carries canonical URL, Open Graph + Twitter card meta (absolute `https://catalogfix.com/...` URLs), and two JSON-LD blocks: `ProfessionalService` and `FAQPage`.
- **Never put the real email address in JSON-LD or meta tags** — it would defeat the ROT13 obfuscation.
- Sections are wrapped in `<main id="main">`; a skip-link is the first element in `<body>`.

## Key CSS Conventions

- CSS custom properties are defined in `:root` at the top of the `<style>` block — always use these, never hardcode hex values
- Layout: `.wrap` = centered container (max 1140px). `.sect` = section padding
- Scroll reveal: add class `rev` to elements that should fade in on scroll. Staggered delays: `rev-d1`, `rev-d2`
- Responsive breakpoints: `800px` (two-col → single col), `600px` (value grid), `820px` (mobile nav)

## Email Obfuscation

The contact email is ROT13-encoded in JS to prevent bot scraping. Located near the bottom of `<script>`:

```js
var enc = 'nqzva@pngnybtsvk.pbz';  // ← ROT13 of admin@catalogfix.com
```

To update: go to rot13.com, encode the new email, paste the result here.

## Design Rules — Always Follow

- **No stock photos** — icons or simple graphics only
- **No gradients** — flat color only
- **No drop shadows** — border or spacing for separation instead
- **No decorative patterns or textures**
- **No hype language** — no "game-changing", "world-class", "cutting-edge"
- **Orange used sparingly** — CTAs, the word "Fix" in the logo/footer, dot markers, and one accent per section max
- White space is intentional — don't crowd layouts

## Voice & Tone

Direct. Confident. No BS. Speak like the expert in the room who doesn't need to impress anyone.

- Explain the *why* behind every recommendation
- Plain language — no jargon for its own sake
- Be honest about what the agency model does and doesn't do
- Never over-promise or imply quick wins
- Approved phrases: "no layers", "direct access", "the person doing the work", "treat it like our own"

## Owner

Carl — founder of CatalogFix. Former PH VA at Amazon agencies. Built the business on fair pay, direct work, and no agency overhead.
