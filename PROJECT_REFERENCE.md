# ConeQt Website: Project Reference

> A guide for making changes to the ConeQt landing page (https://coneqtapp.com).
> Last reviewed: 2026-11-05.
>
> **Tip:** Line numbers drift as you edit. To find a section, search `index.html` for the
> `<!-- ============ NAME ============ -->` markers, an `id="..."`, or a CSS comment such as `/* hero */`.

---

## 1. Overview

| Item | Value |
|---|---|
| Product | ConeQt: a mobile app that connects clients with trusted local workers and services |
| Tagline | "Need it. Connect it." |
| Site type | A static, single-page marketing / waitlist site |
| Tech | Plain HTML, CSS and vanilla JS in **one file**. No framework, no build step, no `package.json` |
| Hosting | Netlify (`coneqtapp.netlify.app`, which redirects to `coneqtapp.com`) |
| Forms | Netlify Forms (the waitlist email capture) |
| Icons | [Lucide](https://lucide.dev) loaded from unpkg, pinned to **v0.344.0** |
| Fonts | Google Fonts: **Plus Jakarta Sans** (English) and **Cairo** (Arabic) |
| Languages | English content with Lebanese Arabic taglines (RTL) |
| Theme | Dark only (navy background, cyan→violet→magenta gradients) |

---

## 2. File Structure

```
coneqt-website/
├── index.html              ← the whole site: <head>, CSS in <style>, HTML, JS in <script>
├── _redirects              ← Netlify redirect rules
├── PROJECT_REFERENCE.md    ← this file
└── assets/
    ├── logo-mark.png             (132 KB) small logo: favicon, apple-touch-icon, nav, footer
    ├── logo.png                  (470 KB) large logo: final CTA section + og:image social preview
    ├── poster-client.jpg         (328 KB) "For clients" card image
    ├── poster-worker.jpg         (343 KB) "For workers" card image
    ├── screen-search-sm.png      (313 KB) hero phone, front (app search screen)
    └── screen-availability-sm.png(160 KB) hero phone, back (app availability screen)
```

### Layout of `index.html`

| Part | What's in it |
|---|---|
| `<head>` | meta/SEO/Open Graph tags, favicon, Google Fonts link |
| `<style>` | all CSS: tokens → components → sections → responsive media queries |
| `<body>` | header/nav → mobile menu → `<main>` (sections) → footer |
| `<script>` (bottom) | Lucide CDN, then the inline JS (categories, availability demo, waitlist, nav, reveal) |

---

## 3. Deployment (Netlify)

- **Publish directory:** the project root (contains `index.html`).
- **Deploying:** drag the folder into Netlify, or push to a connected Git repo. There is nothing to build.
- **`_redirects`** sends the `*.netlify.app` domain to the main domain with a forced 301:
  ```
  https://coneqtapp.netlify.app/*  https://coneqtapp.com/:splat  301!
  http://coneqtapp.netlify.app/*   https://coneqtapp.com/:splat  301!
  ```
  To add a page redirect (for example `/download` to an app store), add a line:
  `/download  https://apps.apple.com/...  302`
- ⚠️ **Every file in the root is published.** That includes this `.md` file, which would be reachable at
  `coneqtapp.com/PROJECT_REFERENCE.md`. If you don't want that, either move this file out of the deploy
  folder or add this line to `_redirects`: `/PROJECT_REFERENCE.md  /  404`

### Waitlist submissions
- Netlify **Dashboard → your site → Forms → `waitlist`** lists every signup email.
- Turn on email notifications under **Site configuration → Notifications → Form submission notifications**.
- Netlify detects the form **at deploy time** from the `data-netlify="true"` attribute. If you rename the form,
  update **both** `name="waitlist"` and the hidden `<input name="form-name" value="waitlist">`.

---

## 4. Design System (CSS variables)

All colours and sizes are defined once in `:root` at the top of `<style>`. **Change them there and every section updates.**

| Token | Value | Used for |
|---|---|---|
| `--bg` | `#050a24` | page background (also `theme-color` meta) |
| `--bg-2` | `#08102f` | availability panel, mockups |
| `--card` | `#0c1538` | cards, FAQ items, chips |
| `--card-2` | `#111c47` | step card gradient, chat bubbles |
| `--line` | `rgba(140,160,255,.14)` | borders |
| `--text` | `#ffffff` | main text |
| `--muted` | `#a6b0d6` | body copy / secondary text |
| `--dim` | `#6f7aa8` | small labels, placeholders |
| `--cyan` | `#22d3ee` | eyebrow labels, checkmarks, accents |
| `--blue` / `--violet` / `--purple` / `--magenta` | `#3b82f6` / `#7c5cff` / `#a855f7` / `#d946ef` | brand palette |
| `--green` | `#10b981` | "available / online" dots |
| `--orange` | `#f59e0b` | (reserved) |
| `--grad` | cyan → blue → violet → magenta | gradient text (`.grad-text`), logo "Q" |
| `--grad-btn` | blue → violet → purple | primary buttons, selected states |
| `--radius` | `22px` | default card corner radius |
| `--max` | `1180px` | max content width (`.wrap`) |

### Icon background colours (`.g-*` classes)
`g-violet`, `g-blue`, `g-cyan`, `g-pink`, `g-green`, `g-orange`. Put one on any `.ic` or `.av` element.

### Reusable classes
| Class | Purpose |
|---|---|
| `.wrap` | centred container with side padding |
| `.sec` | standard section vertical padding |
| `.sec-head` + `.eyebrow` + `h2` + `p` | centred section heading block |
| `.grad-text` | gradient-filled text |
| `.btn .btn-primary` | gradient pill button |
| `.btn .btn-ghost` | outline/transparent button |
| `.reveal` | fade-up animation when scrolled into view |
| `.ar` | Arabic text (Cairo font + RTL) |
| `.cyan` | cyan text colour |

### Fonts
Loaded in `<head>` from Google Fonts. If you add a new weight, add it to that URL
(for example `Plus+Jakarta+Sans:wght@400;500;600;700;800`).

---

## 5. Page Map (top → bottom)

| # | Section | Anchor / id | Marker comment | Key contents |
|---|---|---|---|---|
| 1 | Header / Nav | `#top` | `NAV` | logo, nav links, "Join the waitlist" button, mobile menu (`#mobileMenu`) |
| 2 | Hero | none (`.hero`) | `HERO` | "Launching soon" pill, H1, lead text, Arabic tag, store badges, 2 phone screenshots, orbit + avatar bubbles, 2 floating chips, **4 stats** |
| 3 | Audiences | `#about` | `AUDIENCES` | two cards: **For clients** and **For workers** (image, Arabic quote, translation, checklist, button) |
| 4 | How it works | `#how` | `HOW IT WORKS` | 3 steps (Search / Book / Connect), each with a mini UI mockup |
| 5 | Categories | `#categories` | `CATEGORIES` | two scrolling marquee rows, **generated by JS** from the `cats` array |
| 6 | For workers | `#workers` | `WORKERS` | 3 feature rows + **interactive availability demo** (generated by JS) |
| 7 | Trust band | none | `TRUST` | animated SVG map + 4 trust points |
| 8 | FAQ | `#faq` | `FAQ` | `<details>` accordion items |
| 9 | Final CTA | `#join` | `CTA` | big logo, heading, **waitlist form**, Arabic "قريباً..." |
| 10 | Footer | none | `FOOTER` | logo, tagline, social icons, link columns, © year (auto), Arabic slogan |

**Nav links appear in 3 places.** If you add or rename a section, update all three:
1. `<nav class="nav-links">` (desktop)
2. `<div class="mobile-menu">` (mobile)
3. `<div class="foot-links">` (footer)

---

## 6. How-To Recipes

### 6.1 Change text
Most copy is plain HTML. Search for the sentence you want to change and edit it in place.
- In HTML, write `&` as `&amp;`. (The JS-generated category names handle this for you.)
- Arabic text: keep it inside an element with class `ar` (or `.quote`) so it gets the Cairo font and RTL direction.

### 6.2 Change SEO / social-share preview
In `<head>`:
- `<title>` and `<meta name="description">`: Google result text
- `og:title`, `og:description`, `og:image`: WhatsApp / Facebook / LinkedIn preview
- `og:image` must be an **absolute URL**. A 1200×630 image works best. Today it uses `logo.png`.
- To get a large Twitter/X preview image, change `twitter:card` from `summary` to `summary_large_image`.
- `canonical` and `og:url` should stay `https://coneqtapp.com/`.

### 6.3 Add / remove / rename a service category
In `<script>`, edit the `cats` array. Each entry is `["Display name", "lucide-icon-name"]`:
```js
["Pet services","paw-print"],
```
- Find icon names at https://lucide.dev/icons. The icon must exist in **v0.344.0**; if it doesn't, the slot shows empty.
- Colours are assigned automatically by cycling through `tones`.
- Rows are split in half automatically and duplicated for the seamless loop.
- ⚠️ **The category count is hard-coded in 3 places of text.** Update them when the count changes:
  - Hero stat: `35+` *Service categories*
  - Under the marquee: `<b>36 categories</b>`
  - FAQ: "36 categories, including…"
- Marquee speed: `.track{animation:slide 90s ...}`. A lower number scrolls faster.

### 6.4 Add / edit an FAQ item
Copy an existing block inside `<div class="faq">`:
```html
<details>
  <summary>Your question? <span class="pl"><i data-lucide="plus"></i></span></summary>
  <p>Your answer.</p>
</details>
```
Add `open` to `<details>` to make it expanded by default (only the first one has it now).

### 6.5 Edit the hero stats
In `<div class="stats">`, each stat is:
```html
<div class="stat"><b class="grad-text">35+</b><span>Service categories</span></div>
```
The grid shows 4 columns on desktop and 2 on tablet and mobile. Keep an even count.

### 6.6 Swap images
Replace the file in `assets/` **with the same filename** and nothing else needs to change. Guidelines:
| File | Recommended |
|---|---|
| `screen-*-sm.png` | phone screenshot, about 600px wide, portrait, ideally under 300 KB |
| `poster-*.jpg` | landscape-ish (displayed at 4:3.4, cropped `center 62%`), about 1200px wide, under 350 KB |
| `logo-mark.png` | square, at least 180×180 (used as favicon + apple-touch-icon) |
| `logo.png` | square, displayed as a 150px circle; also the social preview |

**Phone screenshots: hide the status bar (time, battery, signal).** The current screenshots have the top
80px painted over with the app background colour `#020d2b`; the untouched originals are in `assets/originals/`.
Do the same with any new screenshot (in an image editor, or ask Claude to repeat it).

To change which part of a poster is visible, edit `object-position:center 62%` in `.aud .img img`.
Always update the `alt` text if the picture changes.

### 6.7 When the app launches: store buttons
The store badges in the hero are currently plain `<div class="store">` saying "Coming soon on".
When the app is live, change each to a link:
```html
<a class="store" href="https://apps.apple.com/app/..." target="_blank" rel="noopener">
  <svg ...></svg>
  <div><small>Download on the</small><b>App Store</b></div>
</a>
```
Also update everything that says "coming soon":
- the hero pill `Launching soon · قريباً`
- `<meta name="description">` and `og:description` ("Coming soon.")
- FAQ "When does the app launch?"
- CTA heading, paragraph, and "قريباً..."
- the "Join the waitlist" buttons (nav + mobile menu + CTA), which could become "Download the app"

### 6.8 Social links & legal pages
Footer `<div class="socials">` order: Instagram (`@coneqt.lb`), TikTok (`@coneqtlb`), Facebook, LinkedIn, Email.
Instagram and TikTok are live; Facebook, LinkedIn, Email and **Privacy / Terms** still point to `href="#"`.

- **TikTok icon:** Lucide has no TikTok icon, so it's an inline `<svg class="tiktok">` (sized by `.socials svg.tiktok`).
  Use the same approach for any brand Lucide doesn't include (e.g. WhatsApp, X); https://simpleicons.org has the paths.
- To hide an unused icon, delete its `<a>` line.

Replace placeholders with real URLs:
```html
<a href="https://instagram.com/coneqtapp" aria-label="Instagram" target="_blank" rel="noopener">...</a>
<a href="mailto:hello@coneqtapp.com" aria-label="Email">...</a>
```
For Privacy/Terms, create `privacy.html` and `terms.html` in the root, copying the `<head>` and styles,
and link to `/privacy.html` and `/terms.html`. You'll need a privacy policy before collecting emails at scale
and before the app-store submissions.

### 6.9 Change colours / branding
- Edit the tokens in `:root` (section 4).
- A few colours are **hard-coded** outside the tokens and need manual changes if you re-theme:
  the `.g-*` gradients, the hero `.blob` gradients, the SVG gradients inside the orbit and map
  (`<linearGradient>` stops), `.toggle[aria-pressed="true"]` (`#8b4cf6`), `.day .abbr` (`#2a1f6b`),
  and the `rgba(5,10,36,...)` header and menu backgrounds.

### 6.10 Edit the availability demo (For workers section)
In `<script>`, the `days` array is `[short, full name, hours, enabled]`:
```js
["Fri","Friday","09:00 – 15:00",true],
```
It is a visual demo only; nothing is saved. The "Active X of 7 days" counter updates automatically.

### 6.11 Edit the "How it works" mockups
These are pure HTML/CSS inside each `.step > .mock`: fake search results (`.m-row`), a week picker
(`.week`), time slots (`.slots`), and chat bubbles (`.bub.in` / `.bub.out`). Edit the text directly.
Add `class="sel"` to highlight a day or slot.

### 6.12 Edit the map illustration (Trust band)
An inline `<svg class="map" viewBox="0 0 400 320">`. Each worker pin is a `<g class="pin">` with a circle,
initials, and a label pill. To change a label, edit the `<text>` inside it. If the label gets longer,
widen the matching `<rect width="...">` and shift its `x` so it stays centred.

### 6.13 Add a whole new section
1. Copy an existing `<section class="sec" id="...">` block that has a similar layout.
2. Give it a unique `id` and a `<!-- ============ NAME ============ -->` marker.
3. Add `class="reveal"` to elements that should fade in.
4. Add nav links in all 3 places (section 5).
5. Check the responsive breakpoints (section 8).

### 6.14 Add a second waitlist form (for example back in the hero)
The hero used to have a form; its CSS (`.waitlist`, `.form-note`) still exists. Any form works if it:
- has class `js-waitlist`, `data-netlify="true"`, `name="waitlist"`, and the hidden `form-name` input
- is **immediately followed** by `<p class="form-note" aria-live="polite"></p>`, because the JS uses
  `f.nextElementSibling` to show messages.

Copy the whole `<form>…</form>` and the `<p class="form-note">` from the CTA section.

---

## 7. JavaScript Reference

All JS is in the inline `<script>` at the bottom of `index.html`.

| Block | What it does | Depends on |
|---|---|---|
| Categories | builds marquee chips from `cats` into `#row1` / `#row2`; duplicates them (with `aria-hidden`) for the infinite loop | `#row1`, `#row2` |
| Availability demo | renders `days` into `#days`; toggles on click; "Available now" switch | `#days`, `#activeCount`, `#nowToggle`, `#nowCard`, `#nowText` |
| Waitlist | validates email, POSTs form-encoded data to `/` (Netlify Forms), shows success or error in the next `.form-note` | `.js-waitlist` forms |
| Nav | adds `.scrolled` to the header after 10px of scroll; mobile menu open/close | `header`, `#menuBtn`, `#mobileMenu` |
| Reveal | `IntersectionObserver` adds `.in` to `.reveal` elements once visible | `.reveal` |
| Year | fills `#yr` with the current year | `#yr` |
| Icons | `lucide.createIcons()` turns every `<i data-lucide="name">` into an SVG. **It must run last** so the JS-generated icons are included | Lucide CDN |

**Messages users see** (edit inside the waitlist block):
- invalid email: "Please enter a valid email address."
- success: "You're on the list! 🎉 We'll email you as soon as ConeQt is live."
- failure: "Something went wrong. Please try again."

> Note: the comment `// Waitlist forms (front-end only; connect to your backend/email service)` is outdated.
> The form already posts to Netlify Forms.

**Testing locally:** opening `index.html` directly works for everything **except** form submission, which only
works on Netlify. Locally it shows the error message, and that's expected. To test the form, deploy (a deploy preview is fine) and submit there.

---

## 8. Responsive Breakpoints

| Breakpoint | Changes |
|---|---|
| `≤1080px` | phones shrink to 240px |
| `≤920px` (tablet) | desktop nav is hidden, hamburger menu shown; hero, audiences, workers and trust become a single column; hero is centred; stats go to 2 columns |
| `≤600px` (phone) | tighter padding (16px gutters), waitlist form stacks vertically, smaller phones/chips/categories, less section padding |
| `≤360px` | phones shrink to 165px |
| `prefers-reduced-motion` | disables reveal, float, orbit, map, typing and marquee animations; the marquee becomes manually scrollable |

**Always check after changes:** desktop (~1280px), tablet (~800px), phone (~375px).
In the browser, use DevTools (F12) → device toolbar (Ctrl+Shift+M).

---

## 9. Known Placeholders / TODO

- [x] Instagram → `instagram.com/coneqt.lb`, TikTok → `tiktok.com/@coneqtlb`
- [ ] Footer social links still placeholders (Facebook, LinkedIn, Email) → `href="#"`
- [ ] Footer Privacy / Terms → `href="#"` (pages don't exist yet)
- [ ] Store badges are not links yet (wait for launch)
- [ ] Category count mismatch: hero says **35+**, other text says **36** (the array has 36)
- [ ] `og:image` is the square logo; a 1200×630 banner would look better when shared
- [ ] Outdated "front-end only" comment in the waitlist JS
- [ ] Unused leftover CSS: `.waitlist`/`.form-note` hero styles (harmless), and a duplicate `.step::before` rule
- [ ] Consider excluding this `.md` file from the public deploy (section 3)

---

## 10. Pre-Deploy Checklist

- [ ] Page opens with no errors in the browser console (F12 → Console)
- [ ] All icons show (a blank square usually means a misspelled Lucide icon name)
- [ ] Nav links scroll to the right sections (desktop + mobile menu + footer)
- [ ] Layout checked at desktop, tablet and phone widths
- [ ] Arabic text displays right-to-left in the Cairo font
- [ ] Image changes: file sizes are reasonable and `alt` text is updated
- [ ] Category count text matches the `cats` array
- [ ] After deploy: submit a test email and confirm it appears in Netlify → Forms
- [ ] After deploy: check the share preview (for example https://www.opengraph.xyz) if meta tags changed

---

## 11. Change Log

Record notable changes here so you have a history (there's no Git repo yet).

| Date | Change | Notes |
|---|---|---|
| 2026-11-05 | Created this reference document | |
| 2026-11-05 | Removed status bar (time/battery/signal) from both hero phone screenshots | originals backed up in `assets/originals/` |
| 2026-11-05 | Worker pricing changed from "free" to "low-cost monthly subscription" (FAQ + For-workers card checklist) | exact price not stated yet, "shared at launch" |
| 2026-11-05 | Linked Instagram (@coneqt.lb); added TikTok icon + link (@coneqtlb) in footer | |
|  |  |  |
