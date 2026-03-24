# CLAUDE.md

This file provides guidance to Claude Code when working with code in this repository.

## Project

**Lunar Grid Landing Page (v2)** — a single-file HTML landing page for Lunar Grid, a Google Ads campaign generator built by Moonshot Growth.

## Stack

- Single `index.html` file (no build step)
- Font: Manrope (Google Fonts) + JetBrains Mono for code/UI mocks
- Animations: Motion library (`https://esm.sh/motion@11`) for page-load animations, native `IntersectionObserver` for scroll-triggered reveals
- Deploys automatically via GitHub Pages or Cloudflare Pages on push to `master`

## Architecture

### Animation System

Two approaches coexist — use the right one for the context:

1. **Motion library** (`animate`, `stagger`) — used for page-load hero animations and scroll-triggered card/step/metric reveals. Import from `https://esm.sh/motion@11`. Do NOT use Motion's `inView` — it's broken in recent versions.

2. **CSS transitions + class toggle** — used for `.fd-reveal` sections (variant fallbacks, ad preview). A native `IntersectionObserver` adds `.visible` class, CSS handles the transition. This approach is Firefox/Zen-safe.

3. **Vanilla JS** — the trust bar typewriter animation is pure JS with `IntersectionObserver` to start on scroll.

### Scroll Reveal Pattern
```js
// Native IntersectionObserver wrapper (replaces Motion's broken inView)
function onReveal(selector, callback, threshold = 0.1) {
  const targets = document.querySelectorAll(selector);
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) { callback(entry.target); observer.unobserve(entry.target); }
    });
  }, { threshold });
  targets.forEach(el => observer.observe(el));
}
```

### Graceful Degradation

- Scroll-animated elements (`.feat-card`, `.step`, `.metric-card`, `.testi-card`) do NOT have `opacity: 0` in CSS. They're visible by default; Motion enhances with fade-in on scroll. If Motion CDN fails, content is still visible.
- `.fd-reveal` elements use CSS `opacity: 0` + `transform: translateY(28px)` with a `.visible` class transition. If JS fails, these stay hidden — acceptable tradeoff for the smooth animation.
- Hero elements (nav, badge, title words, sub, actions, card) have `opacity: 0` in CSS and are animated immediately on page load by Motion.

### Key CSS Decisions

- Root font-size: `18px` (bumped from 16px for readability)
- UI mock elements (`.hero-card`, `.variant-visual`, `.adp-visual`) use `font-size: 16px` to stay compact
- `.hero-title-line` has `overflow: hidden` + `padding-bottom: 0.15em` for word slide-up animation without clipping descenders
- Sharp corners everywhere (border-radius: 0)

### Responsive Breakpoints

- `960px`: hide nav links, single-column grids, center hero text, shrink nav CTA
- `600px`: smaller container padding, column CTAs (centered), smaller hero title

## Brand

See `STYLE_GUIDE.md` for the full Moonshot Growth brand guide (colors, fonts, logo, design language).

### Quick Reference
- Colors: Scarlet `#E63946`, Saffron `#F4A261`, Blue `#457B9D`, Emerald `#2A9D8F`
- Navy `#1A2544`, Cream `#FAF8F4`
- Font: Manrope (900 for headings, 400-600 for body)
- Logo: Bold "M" + velocity bars icon, "LUNARGRID" wordmark
- Moonshot Growth branding: "by MOONSHOT" in hero, "A Moonshot Growth product" in footer

## Browser Compatibility

- Firefox/Zen: Do NOT use Motion's `inView` function (throws TypeError). Use native `IntersectionObserver` instead. Avoid CSS Grid reordering tricks (`direction: rtl`, `order`, `grid-column`) — use plain DOM order.
- Avoid `@latest` CDN tags — pin to major version (e.g., `motion@11`).
