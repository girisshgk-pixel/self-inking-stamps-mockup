# StampStore — Self Inking Rubber Stamps | Pillar Page Revamp

**Project:** Programmatic SEO — Pillar Page Revamp  
**Client:** StampStore (stamps.net.au)  
**Agency:** AdsPilot  
**Prepared by:** Girish Kumar G | Programmatic SEO Manager — *Father of SEO*  
**Status:** Proposed — Staging Only  
**Target URL:** `stamps.net.au/self-inking-rubber-stamps`  

---

## Repository Files

| File | Description | Size |
|------|-------------|------|
| `self-inking-rubber-stamps.html` | Revamped pillar page — staging mockup | 184 KB |
| `dev-notes-self-inking.html` | Developer implementation notes | 53 KB |
| `README.md` | This file | — |

---

## What This Is

The live page at `stamps.net.au/self-inking-rubber-stamps` currently:
- Ranks **#1** for "self inking rubber stamps" in Australia
- Drives the site's **major revenue**
- Serves only the **DF brand** (31 products)
- Has **zero structured data**, **33 images with no alt text**, and a single-brand H1

This revamp transforms it into a **multi-brand pillar hub** covering all 4 brands while preserving every existing ranking signal.

---

## Pages in This Repo

### 1. `self-inking-rubber-stamps.html` — Pillar Page

The revamped category page. All changes are proposed — nothing is live.

**Brands covered:**

| Brand | Products | Starting Price | Notes |
|-------|----------|---------------|-------|
| DF (StampStore own brand) | 31 | $30.00 | Widest size range, 11 ink colours |
| Trodat | 36 | $32.00 | Austrian-made, industrial grade |
| Colop | 30 | $32.00 | Austrian-made, eco-friendly |
| Trodat Multi-Colour | 18 | $35.00 | Up to 15 colours per impression |
| **Total** | **115** | | |

**Page sections:**

1. Compact Hero — H1, stats bar (115+ products, 4 brands, from $30), dual CTAs
2. Sticky Brand Filter Strip — DF / Trodat / Colop / Multi-Colour tabs
3. Product Grid — all 115 products static in DOM, CSS tab toggle, Show More (8 at a time)
4. Features Strip — Customisable, Fast Shipping, Refillable, Expert Support
5. Brand Cards — 4 brand cards linking to sub-pages
6. Decision Guide — "Choose DF/Trodat/Colop/Multi-Colour if…" 2×2 grid
7. Customer Reviews — 4 verified reviews, 5.0 aggregate
8. FAQ — 7 questions with FAQPage JSON-LD
9. SEO Content — 2-column below-fold copy, ink colour swatches
10. Final CTA — Browse / Custom Design / Phone
11. Footer — brand links, company nav, contact

**Structured Data (4 schemas in `<head>`, static):**

```
BreadcrumbList   — breadcrumb trail in SERP snippet
ItemList         — 16 featured products for product carousel eligibility
FAQPage          — 7 Q&As for FAQ rich result
LocalBusiness    — StampStore, Thomastown VIC, AU
```

**Heading hierarchy:**
```
1 × H1  — Self Inking Rubber Stamps (pillar keyword)
15 × H2 — Brand names, section titles
139 × H3 — Product names, FAQ questions, feature titles
```

**Product image attributes (all 115):**
```
alt   = "Product Full Shot of [product name]"
title = "Buy [product name] — from $[price] | StampStore Australia"
```

**Key technical decisions:**
- All 115 products are **server-rendered static HTML** — not JS-injected, not lazy-loaded per tab
- Brand panels use **CSS `display:none/block` toggle only** — Googlebot reads all products on first crawl
- `initGrid()` hides products 9+ per brand visually on load to protect LCP — all still in DOM
- `loading="lazy"` on images is safe — Google reads `alt` text regardless of render status

**Brand colour:** `#063aa7`  
**Fonts:** Poppins (all weights)  
**Image CDN:** `stamps-storage.syd1.digitaloceanspaces.com/product/image/`

---

### 2. `dev-notes-self-inking.html` — Developer Implementation Notes

Implementation guide for the developer. Built in the BAM (Badge-A-Minit) dev handoff UI style.

**Structure:**

| Section | Topic |
|---------|-------|
| Overview | What this document covers, critical rendering rule |
| 01 | Meta Tags & Robots — existing vs proposed, go-live action |
| 02 | Structured Data — 0 → 4 schemas, static vs JS warning |
| 03 | Heading Hierarchy — H1 change, H2/H3 structure |
| 04 | Hero & Alignment — root cause of desc offset, fix explained |
| 05 | Brand Filter Strip — sticky nav, ARIA tablist |
| 06 | Product Grid — Option A/B/C rendering analysis |
| 07 | Image Alt & Title — 33 missing alts, PHP template pattern |
| 08 | Brand Cards & Decision Guide — internal linking, PAA targeting |
| 09 | Reviews & FAQ — E-E-A-T, FAQPage rich result, CSS accordion |
| 10 | Mobile Responsive — 5 breakpoints table |
| 11 | Sign-off Checklist — 12 go-live items |

Each section shows **Existing Code** (extracted from live page) vs **Proposed Code**, an **SEO Purpose** box explaining the business reason, and callout warnings for critical go-live actions.

---

## Brand Sub-Pages (Linked From Pillar)

These pages already exist on the live site and are linked from the pillar page brand cards and footer:

| Brand | URL |
|-------|-----|
| DF Self Inking Stamps | `stamps.net.au/df-self-inking-stamps` |
| Trodat Self Inking Stamps | `stamps.net.au/trodat-self-inking-stamps` |
| Colop Self Inking Stamps | `stamps.net.au/colop-self-inking-stamps` |
| Trodat Multi-Colour | `stamps.net.au/trodat-multi-coloured-self-inking-stamps` |

---

## Go-Live Checklist

Before pushing `self-inking-rubber-stamps.html` to production:

- [ ] Change `<meta name="robots">` from `noindex,nofollow` to `index,follow`
- [ ] Verify canonical URL resolves correctly (no trailing slash issues)
- [ ] Validate all 4 JSON-LD schemas at [search.google.com/test/rich-results](https://search.google.com/test/rich-results)
- [ ] View page source on staging — confirm all 4 brand panels exist in raw HTML
- [ ] Audit product images — no `<img>` without `alt` in product grid
- [ ] Test brand strip horizontal scroll on 375px and 414px screen widths
- [ ] Test filter chips and price sort on all 4 brand panels
- [ ] Replace hardcoded reviews HTML with dynamic query from review database
- [ ] Remove `.dev-top` dev banner from production template
- [ ] Wire existing site mobile hamburger nav at 767px breakpoint
- [ ] Confirm OG image URL returns 200 and is 1200×630px
- [ ] Run PageSpeed Insights before/after — document LCP, CLS, INP delta

---

## SEO Risk Note

This page currently ranks **#1** for "self inking rubber stamps" in Australia and drives major revenue. All changes in this repository are **proposed and staged only**. Do not push to production without completing the go-live checklist and testing on a staging environment first.

The most critical implementation rule: **all 115 product cards must be server-rendered in the HTML response** — not injected by JavaScript. CSS `display:none` on inactive panels is safe for Google; JS-rendered content on first crawl is not.

---

*Girish Kumar G | Programmatic SEO Manager — Father of SEO*  
*AdsPilot × StampStore*
