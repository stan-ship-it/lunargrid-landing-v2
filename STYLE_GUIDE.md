# Moonshot Growth — Brand Style Guide

## Agency
**Moonshot Growth** is a digital agency. Lunar Grid is one of its products.

## Logo

### Icon (Small "M")
- Bold geometric **M** in navy (`#1A2544`)
- 4 horizontal velocity bars extending right from the M, stacked vertically
- Bar order top→bottom: Flame Scarlet, Saffron, Bleu Électrique, Vert Émeraude
- Bars decrease in width: longest (scarlet) → shortest (emerald)

### Wordmark (Full)
Three variations:
1. **Bars below-left**: "MOONSHOT" text with bars extending left beneath the text
2. **Bars right**: "MOONSHOT" text with bars extending right from the text
3. **Bars down from T**: "MOONSHOT" text with vertical bars dropping from the last letter

### Logo Text
- Font: **Manrope 900** (Black weight)
- All caps: `MOONSHOT`
- Color: Navy `#1A2544`
- Letter-spacing: ~0.05em

## Colors

### Primary Palette
| Name              | Hex       | Usage                                          |
|-------------------|-----------|-------------------------------------------------|
| Flame Scarlet     | `#E63946` | CTAs, highlights, critical actions              |
| Saffron           | `#F4A261` | Google Ads elements, alerts, conversions        |
| Bleu Électrique   | `#457B9D` | Data visualization, dashboards, tracking        |
| Vert Émeraude     | `#2A9D8F` | Success states, validation, growth metrics      |

### Supporting Colors
| Name        | Hex       | Usage                        |
|-------------|-----------|------------------------------|
| Navy        | `#1A2544` | Primary text, dark backgrounds|
| Navy Deep   | `#111C35` | Darker accents               |
| Cream       | `#FAF8F4` | Light backgrounds            |
| White       | `#FFFFFF` | Cards, content areas         |
| Text Muted  | `#6B7694` | Secondary text               |
| Border      | `#E2DDD8` | Borders, dividers            |

## Typography

### Fonts
- **Display / Headings / Logo**: Manrope (weights 700–900)
- **Body**: Manrope (weights 400–600)
- **Code / Mono**: JetBrains Mono (weights 400–500)

## Design Language

### Velocity Bars
The signature brand element. 4 horizontal (or vertical) bars in the primary palette colors, decreasing in length. Used for:
- Logo accent
- Section dividers
- Decorative elements
- Loading/progress indicators

Bar proportions (relative): 100% / 78% / 58% / 40%

### Visual Principles
- **Sharp corners** (border-radius: 0) — no rounded corners on cards or containers
- **Navy + Cream** alternating section backgrounds
- **Flame Scarlet** for primary CTAs and emphasis
- **Grid-based layouts** with generous whitespace
- Animations: smooth easing `cubic-bezier(0.22, 1, 0.36, 1)`, staggered reveals
- Root font-size: 18px for readability; UI mocks use 16px to stay compact

### Animation Patterns
- **Page-load**: Motion library (`animate`, `stagger`) for hero elements
- **Scroll-triggered cards**: Motion `animate` via native `IntersectionObserver` (`onReveal` wrapper)
- **Scroll-triggered detail sections**: Pure CSS transitions (`.fd-reveal` → `.fd-reveal.visible`)
- **Typewriter effect**: Vanilla JS with `IntersectionObserver` trigger, used in trust bar to cycle category names in brand colors
- **Velocity bar draw-in**: Motion `scaleX` animation with `transform-origin: left`

### Trust Bar Typewriter
The trust bar section uses a typewriter animation: "TRUSTED BY AGENCIES MANAGING **{category}**" where the category cycles through E-commerce (scarlet), Real Estate (saffron), Franchises (blue), Local Services (emerald), SaaS & Tech (scarlet) — each typed and deleted in a loop with a blinking cursor.

### CSS Variables (as used in landing page)
```css
:root {
  --scarlet:    #E63946;
  --saffron:    #F4A261;
  --blue:       #457B9D;
  --emerald:    #2A9D8F;
  --navy:       #1A2544;
  --navy-deep:  #111C35;
  --cream:      #FAF8F4;
  --white:      #FFFFFF;
  --text:       #1A2544;
  --text-muted: #6B7694;
  --border:     #E2DDD8;
  --font:       'Manrope', sans-serif;
  --font-mono:  'JetBrains Mono', monospace;
}
```
