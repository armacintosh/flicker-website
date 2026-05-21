# Flicker Website v2 — Design & Engineering Specification

**Project:** Flicker — Butterware Studios  
**Document version:** v1.0  
**Date:** May 2026  
**Sources:** Figma (EC3xwU44Y2PUwDyknQZg9x), Steam Coming Soon Page Copy v4.0, Content Pipeline v2  
**Purpose:** Complete implementation spec for the engineering agent. Build from this document. Do not infer from the Figma alone — the Figma is a starting point, and this spec supersedes it on copy, structure, and social links.

---

## 0. Decisions Made in This Spec

| Question | Decision |
|---|---|
| Trailer CTA | Include "Watch the Trailer" button. It opens a YouTube lightbox modal. Mark the YouTube URL as `[PENDING: gameplay trailer]`. |
| Email capture | No. Steam wishlist is the only conversion action. No sign-up form anywhere on the page. |
| Boss section | Show all 4 named bosses. Blackseadevil gets a mystery/spoiler treatment (name and species visible, sprite partially obscured, description is a tease). |
| Social handles | `@flickergame` across TikTok, Instagram, YouTube. No Discord, no X/Twitter, no Twitch (per Steam v4.0 client direction). |
| Domain | `[PLACEHOLDER: flickergame.com]` — confirm before launch. |
| Design tokens | Colors and fonts extracted from Figma and listed in full below. Engineer should reference this spec for tokens, not re-derive from Figma. |

---

## 1. Site Overview

**What this is:** A single-page marketing website for Flicker, a vertical shoot 'em up by Butterware Studios. The sole conversion goal is getting visitors to wishlist the game on Steam. Everything else — social links, gallery, boss reveals — exists to build desire before that click.

**Voice:** Cute. Creepy. Challenging. The copy is honest, slightly dry, and never oversells. The game is a 5-level, boss-focused shmup. That is worth being proud of. It is not a "next-generation" experience. Write and build accordingly.

**Page filename:** `index.html` (or framework equivalent)  
**Figma reference:** https://www.figma.com/design/EC3xwU44Y2PUwDyknQZg9x/Flicker-%E2%80%94-Website-Design

---

## 2. Design System

### 2.1 Color Tokens

```css
/* Backgrounds */
--color-bg-deep:        #050817;   /* hero, bosses, footer backgrounds */
--color-bg-mid:         #0a0f2c;   /* nav, card image wells, gallery tiles */
--color-bg-card:        #1e1e2e;   /* feature cards, boss cards */
--color-bg-light:       #f5f4fb;   /* about section, gallery section (light alternating) */

/* Brand */
--color-accent-teal:    #00c8b4;   /* badges, links, card borders, highlights */
--color-accent-pink:    #d40072;   /* primary CTA buttons, logo wordmark */
--color-accent-purple:  #8c7ac8;   /* species/scientific name text on boss cards */

/* Text */
--color-text-primary:   #ffffff;
--color-text-muted:     rgba(255, 255, 255, 0.6);
--color-text-dark:      #0a0f2c;   /* headings on light sections */
--color-text-dark-body: #0d0d0d;   /* body copy on light sections */

/* Borders / overlays */
--color-border-teal:    rgba(0, 200, 180, 0.2);
--color-border-solid:   #00c8b4;
--color-nav-bg:         rgba(10, 15, 44, 0.9);
```

### 2.2 Typography

**Font family:** Inter (Google Fonts or locally hosted)  
**Weights used:** 300 (Light), 400 (Regular), 600 (SemiBold), 700 (Bold)

| Role | Weight | Size (desktop) | Size (mobile) | Color |
|---|---|---|---|---|
| Logo / nav wordmark | Bold | 22px | 20px | `--color-accent-pink` |
| Hero tagline | Bold | 52px | 36px | white |
| Hero sub | Regular | 18px | 16px | `--color-text-muted` |
| Section heading (H2) | Bold | 42px on light / 36px on dark | 28–30px | dark or white per section |
| Section badge | SemiBold | 11px, 2px letter-spacing, uppercase | same | `--color-accent-teal` |
| Feature card heading | Bold | 18px | 18px | `--color-accent-teal` |
| Feature / boss body | Regular | 14px | 14px | `--color-text-muted` |
| Boss name | Bold | 16px | 16px | `--color-accent-teal` |
| Boss species | Light | 11px | 11px | `--color-accent-purple` |
| Footer heading | Bold | 13px | 13px | white |
| Footer links | Regular | 13px | 13px | `--color-accent-teal` |
| Copyright | Regular | 12px | 12px | `--color-text-muted` |
| CTA button | Bold | 16px | 16px | white |
| Nav links | Regular | 14px | 14px | `--color-text-muted` |

### 2.3 Spacing & Grid

**Max content width:** 1440px  
**Content padding (desktop):** 80px horizontal  
**Content padding (mobile):** 20px horizontal  
**Section vertical padding (desktop):** 60–80px top/bottom  
**Section vertical padding (mobile):** 48px top/bottom  

Breakpoints:

```
xs:  320px   (min — smallest supported)
sm:  375px   (standard mobile)
md:  768px   (tablet)
lg:  1024px  (small desktop)
xl:  1280px  (standard desktop)
2xl: 1440px  (Figma reference width)
```

Grid system: 12-column, 24px gutter at desktop, 16px gutter at tablet/mobile.

### 2.4 Border Radius & Shadows

```css
--radius-btn:   30px;   /* all CTA buttons — fully rounded pill */
--radius-card:  16px;   /* feature cards, boss cards */
--radius-tile:  10px;   /* gallery tiles, image wells inside cards */
--radius-badge: 6px;    /* section label badges */
--radius-img:   12px;   /* about section gameplay GIF container */
```

No heavy drop shadows. Depth is achieved through background color layering and the `--color-border-teal` borders on cards.

### 2.5 Motion & Animation

**Principle:** Subtle. The game is bioluminescent and atmospheric. Animations should feel like things emerging from darkness, not bouncing in.

| Element | Behavior | Timing |
|---|---|---|
| Section entrance | Fade up 24px on scroll into view | 0.5s ease-out, stagger 0.1s between children |
| Hero CTA buttons | Scale 1.03 on hover | 0.15s ease |
| Nav links | Opacity 1.0 on hover (from 0.6) | 0.15s ease |
| Feature / boss cards | Border color brightens to `--color-border-solid` on hover | 0.2s ease |
| Gallery tiles | Scale 1.02, subtle teal glow box-shadow on hover | 0.2s ease |
| Blackseadevil card | See Section 5.6 — lure pulse animation | Looping, 2s |
| Trailer modal | Fade + scale in from 0.95 | 0.25s ease-out |
| Nav background | Backdrop blur + `--color-nav-bg` appears on scroll past 60px | 0.2s |

**Reduce motion:** Respect `prefers-reduced-motion`. All entrance animations and hover transitions should be disabled or instant when this media query is active.

---

## 3. Asset Inventory

All assets are in Google Drive under the Butterware Studios project folder. Paths are relative to the Drive root.

### 3.1 Existing Assets (ready to use or crop)

| Filename | Drive path | Status | Usage on site |
|---|---|---|---|
| `Flicker_Promo_Art.png` | `Artwork and Logos/Flicker_Promo_Art.png` | EXISTS | Hero full-bleed background, OG image |
| `20241118_Butterware-Flicker_logo3.png` | `Artwork and Logos/20241118_Butterware-Flicker_logo3.png` | EXISTS | Favicon, social profile image |
| `Flicker_Promo_Art-Snailfish.png` | `Artwork and Logos/Flicker_Promo_Art-Snailfish.png` | EXISTS (needs crop) | Mobile hero variant if needed |
| `Begin.gif` | `Pixel Art and Sprites/Mockups/Begin.gif` | EXISTS | About section left panel, Gallery tile 1 |
| `Heroe.gif` | `Pixel Art and Sprites/Mockups/Heroe.gif` | EXISTS | Gallery tile 2 |
| `B1idle_D0.gif` | `Pixel Art and Sprites/Mockups/B1idle_D0.gif` | EXISTS | Gallery tile 3, Boss card 1 (Yeti Crab) |
| `Ani_b5.gif` | `Pixel Art and Sprites/Mockups/Ani_b5.gif` | EXISTS | Gallery tile 4, Boss card 4 (Blackseadevil) |
| `PUps.gif` | `Pixel Art and Sprites/Mockups/PUps.gif` | EXISTS | Could be used as Gallery tile 5 alt |
| `Damage.gif` | `Pixel Art and Sprites/Mockups/Damage.gif` | EXISTS | Optional gallery tile |
| `Boss2PelicanEel.png` | `Pixel Art and Sprites/Bosses/Boss2PelicanEel.png` | EXISTS | Boss card 2 (Pelican Eel) |
| `Boss3Squid_A.png` | `Pixel Art and Sprites/Bosses/Boss3Squid_A.png` | EXISTS | Boss card 3 (Squid) |
| `FinalBossBlackseadevil_A.png` | `Pixel Art and Sprites/Bosses/FinalBossBlackseadevil_A.png` | EXISTS | Boss card 4 (Blackseadevil, obscured) |
| `B04.png` (Yeti Crab idle frame) | `Pixel Art and Sprites/Bosses/Boss1YetiCrab/Boss01 Idle/B04.png` | EXISTS | Boss card 1 (Yeti Crab) |
| Scene frames | `Pixel Art and Sprites/Scenes/Escena_Final/` | EXISTS | Gallery tile 5 |

**Rendering note for all pixel art GIFs and PNGs:** Set `image-rendering: pixelated` (with `-webkit-` prefix). Display at 2x or 3x native resolution. Never use bilinear scaling. This applies to every asset above.

### 3.2 Pending / Needs Creation

| Asset | Purpose | Description for creation |
|---|---|---|
| `gameplay_trailer.mp4` | YouTube trailer (modal CTA) | **PENDING.** 60–90 second gameplay trailer. Cold-open on Yeti Crab appearing. Shows Flicker protagonist in contrast to boss scale in first 10 seconds. Shows perk selection moment. Shows at least 3 boss encounters. Ends on "Wishlist on Steam" card. No narrator voice. Game audio + original soundtrack. Upload to YouTube channel `@flickergame`. |
| `favicon.ico` / `favicon.svg` | Browser tab icon | Export `20241118_Butterware-Flicker_logo3.png` as 32×32 and 180×180 (Apple touch icon). |
| `og-image.png` | Open Graph / social share preview | 1200×630px. Use `Flicker_Promo_Art.png` as background. Overlay "FLICKER" wordmark in `--color-accent-pink` and tagline "Cute. Creepy. Challenging." in white. Safe zone: keep key art within center 800×420px region. |
| `hero-mobile-bg.jpg` | Hero background on mobile | Portrait-crop of `Flicker_Promo_Art.png` at approximately 750×1200px. Keep snailfish protagonist visible and centered. Export as compressed JPG (under 200KB). |

---

## 4. Site Architecture

### 4.1 Single-Page Structure

This is a one-page site. All navigation items anchor-scroll to sections on the same page.

```
/                   index.html
/privacy-policy     privacy.html (minimal, placeholder — can be same domain or link to a hosted policy generator)
```

### 4.2 External Links

| Label | URL | Opens in |
|---|---|---|
| Wishlist on Steam (primary CTA, all instances) | `[PLACEHOLDER: https://store.steampowered.com/app/XXXXX/Flicker/]` | New tab |
| Watch the Trailer | `[PLACEHOLDER: https://www.youtube.com/watch?v=XXXXX]` | Lightbox modal (same page) |
| App Store | `[PLACEHOLDER: App Store URL]` | New tab |
| Google Play | `[PLACEHOLDER: Google Play URL]` | New tab |
| TikTok | `https://www.tiktok.com/@flickergame` | New tab |
| Instagram | `https://www.instagram.com/flickergame` | New tab |
| YouTube | `https://www.youtube.com/@flickergame` | New tab |
| Privacy Policy | `/privacy-policy` | Same tab |

**Note:** All `[PLACEHOLDER]` URLs must be confirmed and replaced before launch. The Steam URL is the most critical — every CTA on the page points to it.

### 4.3 Social Handles

**Confirmed handle across all platforms:** `@flickergame`  
**Platforms:** TikTok, Instagram, YouTube  
**Not included:** Discord, X/Twitter, Twitch (removed per client direction in Steam v4.0)

---

## 5. Section-by-Section Specification

Section order (top to bottom):

1. Navigation
2. Hero
3. About the Game
4. Features (Why Flicker?)
5. Gallery / Media
6. Meet the Bosses
7. Footer

Alternating background rhythm: **dark → light → dark → light → dark → dark**
Specifically: Hero (dark) → About (light) → Features (dark) → Gallery (light) → Bosses (dark) → Footer (dark)

---

### S1. Navigation

**Background:** `--color-nav-bg` (`rgba(10, 15, 44, 0.9)`) with `backdrop-filter: blur(12px)`  
**Position:** `position: sticky; top: 0; z-index: 100`  
**Height:** 72px desktop, 60px mobile  
**Border bottom:** `1px solid rgba(0, 200, 180, 0.15)` — appears on scroll past 60px, hidden at top of page

**Desktop layout (≥1024px):**

```
[LOGO wordmark]          [About] [Features] [Gallery] [Bosses]          [♥ Wishlist on Steam]
left: 40px               centered nav group                              right: 40px
```

- **Logo:** Text "FLICKER" in Inter Bold 22px `--color-accent-pink`. Links to `#hero` (smooth scroll to top). This is a text wordmark, not the PNG logo.
- **Nav links:** About, Features, Gallery, Bosses. Each smooth-scrolls to the corresponding section anchor. Inter Regular 14px `--color-text-muted`. On hover: opacity 1.0 (0.15s ease). Active section: `--color-accent-teal`.
- **Nav CTA button:** "♥ Wishlist on Steam". Pill button (`--radius-btn`). Background `--color-accent-pink`. Text white, Inter Bold 16px. Width 220px, height 48px. Links to Steam wishlist URL (new tab). On hover: brightness 1.1.

**Mobile layout (<1024px):**

```
[LOGO]                                                    [☰ hamburger]
```

- Hamburger icon (3 lines or equivalent). On tap, a full-width slide-down menu appears beneath the nav bar containing:
  - Stacked nav links: About, Features, Gallery, Bosses — each 48px tap target
  - "♥ Wishlist on Steam" pill button, full width, below links
  - Close: tap hamburger again, or tap outside, or tap any link (auto-close after navigation)
- Menu background: `--color-bg-mid` with blur
- Menu animation: slide down from nav bar, 0.2s ease-out

**Scroll behavior:** On scroll past 60px, the nav border-bottom appears and backdrop-blur intensifies. At top of page, nav is borderless (blends with hero).

**Section anchor IDs:**

```html
id="about"
id="features"
id="gallery"
id="bosses"
```

---

### S2. Hero

**Section ID:** `hero` (page root / top of scroll)  
**Background:** `--color-bg-deep` (#050817) base. Full-bleed `Flicker_Promo_Art.png` as background image, `background-size: cover; background-position: center`.  
**Height:** 100vh minimum, 900px maximum on desktop. On mobile, min-height 600px.  
**Overlay:** Gradient overlay on top of promo art. See gradient spec below.

**Hero gradient overlay:**

```css
background: linear-gradient(
  to bottom,
  rgba(5, 8, 23, 0.3) 0%,
  rgba(5, 8, 23, 0.5) 40%,
  rgba(5, 8, 23, 0.85) 75%,
  rgba(5, 8, 23, 1.0) 100%
);
```

This ensures legibility of text at the bottom of the hero while letting the promo art breathe in the upper portion.

**Content alignment:** Vertically centered within the hero, slightly lower than true center (centered at 55–60% height). Horizontally centered.

**Hero content (top to bottom):**

1. **Tagline** (H1)
   - Text: "One tiny fish. Five levels of things that want to stop her."
   - Style: Inter Bold, 52px desktop / 36px mobile / 28px on xs
   - Color: white
   - Width: max 680px, centered
   - Line height: 1.15

2. **Sub-headline**
   - Text: "A fast-paced underwater shoot 'em up — coming to Steam, iOS & Android."
   - Style: Inter Regular, 18px desktop / 16px mobile
   - Color: `--color-text-muted`
   - Width: max 600px, centered
   - Margin top: 24px

3. **CTA row** (two buttons side by side, centered)
   - Margin top: 48px
   - Gap between buttons: 16px
   - Stack vertically on mobile (320–767px)

   **Primary CTA — "♥ Wishlist on Steam"**
   - Background: `--color-accent-pink` (#d40072)
   - Text: white, Inter Bold 16px
   - Size: 230×54px desktop, 100% width mobile
   - Border radius: `--radius-btn` (30px)
   - Link: Steam wishlist URL, new tab
   - Hover: brightness 1.1, scale 1.03

   **Secondary CTA — "▶ Watch the Trailer"**
   - Background: `--color-bg-mid` (#0a0f2c)
   - Border: 2px solid white
   - Text: white, Inter Bold 16px
   - Size: 210×54px desktop, 100% width mobile
   - Border radius: `--radius-btn` (30px)
   - Action: Opens YouTube lightbox modal (see Section 7.2)
   - **Status flag:** `data-status="pending-trailer"` — when YouTube URL is not yet set, this button should still render but the click handler should be a no-op or show a brief "Coming soon" tooltip. Do not hide the button.
   - Hover: border-color `--color-accent-teal`, scale 1.03

4. **Scroll hint**
   - Text: "↓ scroll"
   - Style: Inter Regular, 13px, `--color-text-muted`
   - Position: Centered, 32px above bottom of hero section
   - Subtle fade animation: opacity pulses 0.4 → 0.8 → 0.4 on a 2s loop
   - Hide on mobile (below 768px)

**Background image notes:**
- Desktop: `Flicker_Promo_Art.png`, full bleed, `object-fit: cover`
- Mobile: Use `hero-mobile-bg.jpg` (portrait crop, PENDING creation) at viewports below 768px. If not yet available at build time, fall back to `Flicker_Promo_Art.png` with `background-position: center top`
- Preload the hero background image: add `<link rel="preload" as="image">` in `<head>`

---

### S3. About the Game

**Section ID:** `about`  
**Background:** `--color-bg-light` (#f5f4fb) — this is a light section  
**Padding:** 60px top, 80px bottom desktop; 48px top/bottom mobile  

**Desktop layout:** Two-column, 50/50 split with 40px gap. Left column: gameplay GIF. Right column: text content. Max content width 1440px, padding 80px horizontal.

**Left column — Gameplay GIF panel:**

- Container: 560×460px desktop. Dark background `--color-bg-mid`. Border radius `--radius-img` (12px). `overflow: hidden`.
- Asset: `Begin.gif` — displayed at 2x or 3x native resolution, `image-rendering: pixelated`
- The GIF should fill the container horizontally and be vertically centered
- On mobile: this column renders full width above the text column, max-height 240px, maintains aspect ratio

**Right column — Text content:**

1. **Section badge**
   - Text: "ABOUT THE GAME"
   - Style: Inter SemiBold, 11px, 2px letter-spacing, `--color-accent-teal`
   - Container: pill/badge with `border: 1px solid --color-border-solid`, background `rgba(0, 200, 180, 0.2)`, border-radius `--radius-badge`, padding 10px 16px
   - Margin bottom: 16px

2. **Heading (H2)**
   - Text: "The deep ocean is beautiful. It also wants you dead."
   - Style: Inter Bold, 42px desktop / 30px mobile
   - Color: `--color-text-dark` (#0a0f2c)
   - Line height: 1.2
   - Margin bottom: 24px

3. **Body copy**
   - Paragraph 1: "Flicker is a vertical shoot 'em up where you pilot an adorable snailfish through 5 levels of increasingly dangerous deep-sea territory. Dodge bullet storms, discover power-ups, and face off against some of the ocean's most terrifying real-world creatures — the ones nature already made into nightmares."
   - Paragraph 2: "Beautiful hand-crafted bioluminescent pixel art, original music for every level, and bosses that are genuinely unsettling. Available on Steam, iOS, and Android."
   - Style: Inter Regular, 15px, line-height 1.7
   - Color: `--color-text-dark-body` (#0d0d0d)
   - Margin between paragraphs: 16px

4. **Inline CTA link**
   - Text: "See it in action  ↓"
   - Style: Inter SemiBold, 14px, `--color-accent-pink`
   - Links to: smooth scroll to `#gallery`
   - Margin top: 32px
   - Hover: underline

**Mobile layout:** Single column. Badge → Heading → Body → CTA link. GIF panel above, full width, 240px tall. Text below with 24px gap.

---

### S4. Features (Why Flicker?)

**Section ID:** `features`  
**Background:** `--color-bg-mid` (#0a0f2c) — dark section  
**Padding:** 60px top, 80px bottom desktop; 48px top/bottom mobile  

**Section header (centered):**

1. **Section badge**
   - Text: "WHY FLICKER?"
   - Same badge style as S3

2. **Section heading (H2)**
   - Text: "Three reasons to dive in."
   - Style: Inter Bold, 28px, white, centered
   - Margin top: 16px, margin bottom: 48px

**Feature cards row:** 3 cards in a row on desktop. Stack to single column on mobile. Each card 400×260px desktop, full-width mobile.

Card style:
- Background: `--color-bg-card` (#1e1e2e)
- Border: `1px solid --color-border-teal` (`rgba(0, 200, 180, 0.2)`)
- Border radius: `--radius-card` (16px)
- Padding: 24px
- On hover: border brightens to `--color-border-solid` (#00c8b4), 0.2s ease

**Card 1 — Fast & Frantic**
- Icon: ⚡ (32px)
- Heading: "Fast & Frantic" — Inter Bold 18px, `--color-accent-teal`
- Body: "5 levels of escalating bullet patterns, power-ups, and enemies designed to test your reflexes — not your patience." — Inter Regular 14px, `--color-text-muted`

**Card 2 — Real Monsters**
- Icon: 🦀 (32px)
- Heading: "Real Monsters" — Inter Bold 18px, `--color-accent-teal`
- Body: "Every boss is a real deep-sea creature. The Yeti Crab. The Pelican Eel. The Squid. The Blackseadevil. Nature did the hard work." — Inter Regular 14px, `--color-text-muted`

**Card 3 — Original Soundtrack**
- Icon: 🎵 (32px)
- Heading: "Original Soundtrack" — Inter Bold 18px, `--color-accent-teal`
- Body: "A full original score composed for every level and boss encounter. Sounds great with the volume up." — Inter Regular 14px, `--color-text-muted`

**Mobile layout:** Cards stack vertically with 16px gap. Full width minus 40px horizontal padding.

**Desktop card gap:** (1440 - 160 - 1200) / 2 = ~40px gap between cards, or use CSS gap on a flex row.

---

### S5. Gallery / Media

**Section ID:** `gallery`  
**Background:** `--color-bg-light` (#f5f4fb) — light section  
**Padding:** 60px top, 60px bottom desktop; 48px top/bottom mobile  

**Section header (centered):**

1. **Section badge:** "MEDIA" (same badge style)

2. **Section heading (H2):**
   - Text: "See it in action"
   - Style: Inter Bold, 36px, `--color-text-dark`, centered
   - Margin bottom: 40px

**Gallery tiles:** 5 tiles in a horizontal row on desktop. Horizontal scroll on tablet/mobile.

**Desktop tile layout:**
- Each tile: 230×340px
- Gap between tiles: 10px
- Container: full width, 80px horizontal padding, `display: flex; gap: 10px`

**Mobile / tablet layout:**
- Container: `overflow-x: auto; scroll-snap-type: x mandatory; -webkit-overflow-scrolling: touch`
- Each tile: `min-width: 200px; scroll-snap-align: start`
- Show 1.5 tiles at a time on mobile to hint at scrollability
- Scroll indicator dots below the tiles (5 dots, active dot fills to `--color-accent-teal`)

**Each tile style:**
- Background: `--color-bg-mid` (#0a0f2c)
- Border: `1px solid --color-border-teal`
- Border radius: `--radius-tile` (10px)
- `overflow: hidden`
- On hover: scale 1.02, `box-shadow: 0 0 16px rgba(0, 200, 180, 0.25)`, 0.2s ease
- Cursor: pointer (all tiles expand to lightbox or fullscreen on click — see Section 7.5)

**Tile content:** GIF / image fills the tile. `image-rendering: pixelated`. `object-fit: contain` with dark background. A small label overlaid at the bottom (optional, only visible on hover):
- Background: `rgba(10, 15, 44, 0.85)`, bottom of tile, 36px tall
- Text: caption (see below), Inter Regular 12px, `--color-accent-teal`, centered

**Tile 1 — Gameplay Level 1**
- Asset: `Begin.gif`
- Caption: "Gameplay — Level 1"

**Tile 2 — Hero Animation**
- Asset: `Heroe.gif`
- Caption: "Flicker — Character Sprite"

**Tile 3 — Yeti Crab**
- Asset: `B1idle_D0.gif`
- Caption: "The Yeti Crab — Boss 1"

**Tile 4 — Final Boss**
- Asset: `Ani_b5.gif`
- Caption: "The Abyss — Boss 4"

**Tile 5 — Scene / Environment**
- Asset: Scene frame from `Pixel Art and Sprites/Scenes/Escena_Final/` — use the most visually complete single frame available
- If a suitable static frame is not available, substitute `PUps.gif` (perk selection screen) with caption "Perk Selection"
- Caption: "Deep Ocean — Environment"

---

### S6. Meet the Bosses

**Section ID:** `bosses`  
**Background:** `--color-bg-deep` (#050817) — dark section  
**Padding:** 60px top, 80px bottom desktop; 48px top/bottom mobile  

**Section header (centered):**

1. **Section badge:** "MEET THE BOSSES"

2. **Section heading (H2):**
   - Text: "Meet the Bosses"
   - Style: Inter Bold, 36px, white, centered
   - Margin bottom: 8px

3. **Section sub:**
   - Text: "They're real. They're enormous. They live at the bottom of the ocean."
   - Style: Inter Regular, 16px, `--color-text-muted`, centered
   - Margin bottom: 48px

**Boss cards row:** 4 cards in a horizontal row on desktop. 2×2 grid on tablet (768–1023px). Single column on mobile (<768px).

**Card dimensions:** 310×460px desktop. Full width on mobile with max-width 340px, centered.

**Standard boss card style:**
- Background: `--color-bg-card` (#1e1e2e)
- Border: `1px solid --color-border-teal`
- Border radius: `--radius-card` (16px)
- Padding: 20px
- `overflow: hidden`
- On hover: border brightens to `--color-border-solid`, 0.2s

**Card internal structure:**
1. **Sprite image well:** 270×240px, background `--color-bg-mid`, border-radius `--radius-tile` (10px), margin-bottom 16px. Asset displayed at 2x, `image-rendering: pixelated`, `object-fit: contain`.
2. **Boss name:** Inter Bold, 16px, `--color-accent-teal`
3. **Species (scientific name):** Inter Light, 11px, `--color-accent-purple` (#8c7ac8). Italicized.
4. **Description:** Inter Regular, 12px, `--color-text-muted`, line-height 1.6

---

**Card 1 — The Yeti Crab**
- Asset: `Pixel Art and Sprites/Bosses/Boss1YetiCrab/Boss01 Idle/B04.png`
- Name: "The Yeti Crab"
- Species: *Kiwa hirsuta*
- Description: "Blind. Covered in hair-like filaments. Lives near hydrothermal vents. Flicker's first major problem."

**Card 2 — The Pelican Eel**
- Asset: `Boss2PelicanEel.png`
- Name: "The Pelican Eel"
- Species: *Eurypharynx pelecanoides*
- Description: "Its jaw unhinges to swallow prey larger than itself. It finds this completely normal."

**Card 3 — The Squid**
- Asset: `Boss3Squid_A.png`
- Name: "The Squid"
- Species: *Species TBD — update when confirmed*
- Description: "Fast. Multi-armed. Not interested in negotiating."

**Card 4 — The Blackseadevil (MYSTERY TREATMENT)**

This card is intentionally different from the other three to tease the final boss. Follow these specifications exactly.

- Asset: `Ani_b5.gif` — displayed but with a heavy overlay (see below)
- Name: "???" — DO NOT show "The Blackseadevil" here
- Species: hidden
- Description: "What lives at the very bottom of the ocean? You'll find out."

**Mystery overlay on sprite well:**
- The sprite image well gets an additional absolute-positioned overlay layer on top of the GIF
- Overlay: `background: radial-gradient(ellipse at center, rgba(5, 8, 23, 0) 20%, rgba(5, 8, 23, 0.92) 100%)` — this creates a vignette that obscures the outer form of the sprite but leaves a glowing center visible
- Additionally: a single pulsing bioluminescent "lure light" dot (CSS-only or from the GIF's existing lure animation) should be visible through the darkness
  - Size: 8px circle, `--color-accent-teal`
  - Animation: `opacity: 0.4` to `opacity: 1.0`, 2s ease-in-out, infinite, alternate
- A "?" icon or lock icon (SVG, 24×24px, `--color-text-muted`) is centered over the sprite well
- Boss name rendered as three "???" characters in Inter Bold 16px, `--color-text-muted` (not teal like the others)
- Species field hidden entirely (no placeholder text)

**Boss section note (reconciling 5 levels vs. 4 bosses):** The website displays 4 bosses as designed. Copy says "5 levels" throughout, which is accurate — not every level has a boss. This is consistent with the Steam v4.0 copy. Do not add a "5th boss card" placeholder.

---

### S7. Footer

**Background:** `--color-bg-deep` (#050817) — continuous with Bosses section  
**Top border:** `1px solid rgba(255, 255, 255, 0.08)` — subtle separator from bosses  
**Padding:** 60px top, 40px bottom desktop; 48px top/bottom mobile  

**Desktop layout:** Three-column layout across full width (80px side padding).

```
[Left column]              [Center column]          [Right column]
Logo + studio tagline      Follow Us                Get the Game
                           Social links             Store links
```

**Left column (~300px):**
- Logo wordmark: "FLICKER" in Inter Bold 28px, `--color-accent-pink`
- Studio tagline (two lines):
  - Line 1: "A game by Butterware Studios"
  - Line 2: "Toronto, Canada"
  - Style: Inter Regular 14px, `--color-text-muted`, line-height 1.8
  - Margin top: 12px

**Center column (~200px, horizontally centered in page):**
- Heading: "Follow Us" — Inter Bold 13px, white, margin-bottom 16px
- Links (each on its own line, 24px line height):
  - → TikTok — links to `https://www.tiktok.com/@flickergame`, new tab
  - → Instagram — links to `https://www.instagram.com/flickergame`, new tab
  - → YouTube — links to `https://www.youtube.com/@flickergame`, new tab
- All links: Inter Regular 13px, `--color-accent-teal`
- On hover: underline, opacity 0.8

**Right column (~200px, right-aligned):**
- Heading: "Get the Game" — Inter Bold 13px, white, margin-bottom 16px
- Links:
  - → Steam — Wishlist — links to Steam wishlist URL, new tab
  - → App Store — `[PLACEHOLDER]`, new tab
  - → Google Play — `[PLACEHOLDER]`, new tab
- Same link style as center column

**Footer rule (bottom):**
- `1px solid rgba(255, 255, 255, 0.08)` — horizontal rule above copyright row
- Margin: 40px top

**Copyright row:**
- Left: "© 2026 Butterware Studios. All rights reserved." — Inter Regular 12px, `--color-text-muted`
- Right: "Privacy Policy" — Inter Regular 12px, `--color-accent-teal`, links to `/privacy-policy`

**Mobile footer layout:**
- Stack all three columns vertically
- Order: Logo/studio → Follow Us → Get the Game → footer rule → copyright
- Each section separated by 32px margin
- Copyright row: stacked (copyright line above, Privacy Policy link below), both left-aligned

---

## 6. Mobile-First Responsive Behavior

Build mobile-first. The following table summarizes the key layout changes per section at each breakpoint.

| Section | Mobile (<768px) | Tablet (768–1023px) | Desktop (≥1024px) |
|---|---|---|---|
| Nav | Logo + hamburger menu | Logo + collapsed links | Full horizontal nav |
| Hero | Single column, stacked CTAs, no scroll hint, 600px min-height | Single column, side-by-side CTAs | Full two-CTA layout, 100vh |
| About | GIF full-width (240px tall) above text | GIF left (50%), text right | Two-column 50/50 |
| Features | Single-column card stack | 2-col + 1-col below (or 3-col if width allows) | 3-column row |
| Gallery | Horizontal scroll strip, 1.5 tiles visible | 3-tile visible + scroll | 5-tile full-width row |
| Bosses | Single-column stack, centered | 2×2 grid | 4-column row |
| Footer | Stacked columns | Stacked columns | 3-column horizontal |

**Touch targets:** All interactive elements — buttons, links, nav items — minimum 44×44px tap area.

**Images:** All `<img>` elements should have `loading="lazy"` except the hero background (which should preload) and the logo.

**Typography scaling:** Use CSS `clamp()` for fluid headings where appropriate. Example for hero tagline:

```css
font-size: clamp(28px, 5vw, 52px);
```

---

## 7. Interactive Behaviors

### 7.1 Smooth Scroll

All anchor links (`#about`, `#features`, `#gallery`, `#bosses`) trigger `scroll-behavior: smooth` on the `<html>` element. Set `scroll-margin-top: 80px` on each section ID so the sticky nav does not obscure the section heading on arrival.

### 7.2 Trailer Modal (YouTube Lightbox)

Triggered by: clicking "▶ Watch the Trailer" button in Hero.

**Modal structure:**
- Full-screen overlay: `rgba(5, 8, 23, 0.92)` background
- Overlay click closes modal
- Center: responsive iframe container — 16:9 aspect ratio, max-width 900px
- YouTube embed URL: `[PLACEHOLDER: https://www.youtube.com/embed/VIDEO_ID?autoplay=1&rel=0]`
- Close button: "✕" in top-right corner, 40×40px, white, Inter Regular 20px
- Keyboard: `Escape` key closes modal
- Focus trap: while modal is open, focus must remain inside modal (accessibility requirement)
- Animation: fade in overlay 0.2s, scale iframe container from 0.95 to 1.0 over 0.25s ease-out

**Pending state behavior:** Until the YouTube URL is available, clicking "Watch the Trailer" should render the button as normal but trigger a tooltip or inline message: "Trailer coming soon." Do not disable or hide the button. Do not navigate anywhere.

### 7.3 Hover States

| Element | Hover state |
|---|---|
| Primary CTA (pink button) | `filter: brightness(1.1)`, `transform: scale(1.03)` |
| Secondary CTA (bordered) | `border-color: --color-accent-teal`, `transform: scale(1.03)` |
| Nav links | `color: white` (from muted) |
| Nav CTA | `filter: brightness(1.1)` |
| Feature cards | `border-color: --color-border-solid` |
| Gallery tiles | `transform: scale(1.02)`, `box-shadow: 0 0 16px rgba(0, 200, 180, 0.25)` |
| Boss cards (1, 2, 3) | `border-color: --color-border-solid` |
| Boss card 4 (mystery) | `border-color: rgba(0, 200, 180, 0.4)` — slightly brighter but still not full teal |
| Footer links | `text-decoration: underline`, `opacity: 0.8` |
| "See it in action" CTA | `text-decoration: underline` |

All transitions: `transition: [property] 0.15–0.2s ease`.

### 7.4 Scroll Entrance Animations

Use `IntersectionObserver` with `threshold: 0.15`. When a section enters the viewport, trigger a fade-up animation on its children.

```css
.animate-on-scroll {
  opacity: 0;
  transform: translateY(24px);
  transition: opacity 0.5s ease-out, transform 0.5s ease-out;
}
.animate-on-scroll.visible {
  opacity: 1;
  transform: translateY(0);
}
```

Apply staggered delay to sibling children:

```css
.animate-on-scroll:nth-child(1) { transition-delay: 0s; }
.animate-on-scroll:nth-child(2) { transition-delay: 0.1s; }
.animate-on-scroll:nth-child(3) { transition-delay: 0.2s; }
```

Elements to animate: section badges, headings, body text blocks, feature cards (each staggered), boss cards (each staggered), gallery tiles.

Respect `prefers-reduced-motion`: when this media query matches, set all `transition-duration` and `animation-duration` to `0s`.

### 7.5 Gallery Tile Interaction

On click or tap, each gallery tile expands to a lightbox (similar to the trailer modal):
- Full-screen dark overlay
- The GIF / image displayed at maximum comfortable size (max 80vw × 80vh)
- `image-rendering: pixelated` preserved
- Caption label visible below the image
- Close on overlay click, close button (top-right), or `Escape`

### 7.6 Active Nav Highlight

Use `IntersectionObserver` to detect the currently visible section. The corresponding nav link becomes `--color-accent-teal` (from `--color-text-muted`). Transition 0.2s.

---

## 8. SEO & Meta Tags

Place the following in `<head>`:

```html
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Flicker — A Deep-Sea Shoot 'Em Up by Butterware Studios</title>
<meta name="description" content="One tiny snailfish. Five levels of real deep-sea bosses. Wishlist Flicker on Steam — a cute, creepy, challenging vertical shoot 'em up from Butterware Studios.">

<!-- Open Graph -->
<meta property="og:title" content="Flicker — A Deep-Sea Shoot 'Em Up">
<meta property="og:description" content="Pilot a tiny snailfish through 5 levels of real deep-sea horrors. Cute. Creepy. Challenging. Wishlist on Steam.">
<meta property="og:image" content="[PLACEHOLDER: /assets/og-image.png]">
<meta property="og:image:width" content="1200">
<meta property="og:image:height" content="630">
<meta property="og:url" content="[PLACEHOLDER: https://flickergame.com]">
<meta property="og:type" content="website">
<meta property="og:site_name" content="Flicker">

<!-- Twitter / X card (keep even though X is not a social link — for share previews) -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="Flicker — A Deep-Sea Shoot 'Em Up">
<meta name="twitter:description" content="Pilot a tiny snailfish through 5 levels of real deep-sea horrors. Cute. Creepy. Challenging.">
<meta name="twitter:image" content="[PLACEHOLDER: /assets/og-image.png]">

<!-- Favicon -->
<link rel="icon" type="image/x-icon" href="/favicon.ico">
<link rel="apple-touch-icon" href="/apple-touch-icon.png">

<!-- Font preload -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">

<!-- Hero image preload -->
<link rel="preload" as="image" href="/assets/Flicker_Promo_Art.png">
```

**Canonical URL:** `<link rel="canonical" href="[PLACEHOLDER: https://flickergame.com]">`

---

## 9. Accessibility

- All images must have descriptive `alt` text. GIFs with animation: `alt="[Boss name] animated pixel art sprite"`. The mystery boss card image: `alt="A dark ocean abyss — final boss hidden"`.
- All interactive elements must be keyboard-navigable with visible `:focus` styles. Focus style: `outline: 2px solid --color-accent-teal; outline-offset: 3px`.
- Color contrast: all body text on dark backgrounds must meet WCAG AA (4.5:1 minimum). The muted text (`rgba(255,255,255,0.6)`) on `#050817` passes. Verify programmatically.
- Modal dialogs: `role="dialog"`, `aria-modal="true"`, `aria-label="[Trailer / Gallery image]"`. Focus trap required.
- Hamburger menu: `aria-expanded="false/true"`, `aria-controls="mobile-nav"`, `aria-label="Open navigation menu"`.
- Section headings must follow a logical H1 → H2 → H3 hierarchy. The Hero tagline is H1. All section headings are H2. Boss names and feature card headings are H3.
- Animated GIFs: Respect `prefers-reduced-motion` — pause GIF animation when this media query matches (use a static first frame if possible, or set the GIF `src` to empty and replace with a static PNG).
- Steam wishlist links that open in a new tab: include `aria-label="Wishlist Flicker on Steam (opens in new tab)"`.

---

## 10. Open Items & Engineering Flags

These must be resolved before launch. The site can be built and staged with placeholders; replace these before going live.

| # | Item | Owner | Priority |
|---|---|---|---|
| 1 | Steam wishlist URL — replace all `[PLACEHOLDER: https://store.steampowered.com/app/XXXXX/Flicker/]` with live URL | Butterware | CRITICAL |
| 2 | YouTube trailer URL — replace `[PLACEHOLDER]` in modal and update `data-status="pending-trailer"` handler | Butterware | HIGH |
| 3 | Domain confirmation — is the site `flickergame.com` or another URL? | Butterware | HIGH |
| 4 | `og-image.png` creation — 1200×630px described in Section 3.2 | Designer | HIGH |
| 5 | `hero-mobile-bg.jpg` — portrait crop of promo art for mobile hero | Designer | MEDIUM |
| 6 | App Store URL | Butterware | MEDIUM |
| 7 | Google Play URL | Butterware | MEDIUM |
| 8 | `FinalBossBlackseadevil_A.png` used in mystery card — confirm the asset name is exactly this. If the GIF `Ani_b5.gif` provides better visual material for the lure-pulse effect, use the GIF instead of the PNG for the Blackseadevil sprite well. | Engineer | MEDIUM |
| 9 | Boss 3 Squid species name — currently "Species TBD" in Figma. Update to correct scientific name when confirmed. | Butterware | LOW |
| 10 | Privacy Policy page content — placeholder at `/privacy-policy` is sufficient for launch but must be populated before any live user data is collected (e.g., if email capture is added later) | Butterware / Legal | LOW |
| 11 | Gallery tile 5 — confirm which scene frame from `Escena_Final/` folder is the preferred single image. If none is usable, fall back to `PUps.gif` per Section 5.5. | Butterware | LOW |
| 12 | Hero tagline final text — Figma says "Ten levels," Steam v4.0 says "Five levels." This spec uses "Five levels" per Steam v4.0 as the authoritative document. Confirm this is correct before launch. | Butterware | CONFIRM |

---

## 11. Copy Reference (Final Approved, Ready to Paste)

All copy below is reconciled from Steam v4.0 and supersedes any text visible in the Figma file.

**Hero tagline:** One tiny fish. Five levels of things that want to stop her.  
**Hero sub:** A fast-paced underwater shoot 'em up — coming to Steam, iOS & Android.  
**Primary CTA:** ♥ Wishlist on Steam  
**Secondary CTA:** ▶ Watch the Trailer  

**About heading:** The deep ocean is beautiful. It also wants you dead.  
**About body P1:** Flicker is a vertical shoot 'em up where you pilot an adorable snailfish through 5 levels of increasingly dangerous deep-sea territory. Dodge bullet storms, discover power-ups, and face off against some of the ocean's most terrifying real-world creatures — the ones nature already made into nightmares.  
**About body P2:** Beautiful hand-crafted bioluminescent pixel art, original music for every level, and bosses that are genuinely unsettling. Available on Steam, iOS, and Android.  
**About CTA link:** See it in action ↓  

**Features heading:** Three reasons to dive in.  
**Feature 1:** Fast & Frantic — 5 levels of escalating bullet patterns, power-ups, and enemies designed to test your reflexes — not your patience.  
**Feature 2:** Real Monsters — Every boss is a real deep-sea creature. The Yeti Crab. The Pelican Eel. The Squid. The Blackseadevil. Nature did the hard work.  
**Feature 3:** Original Soundtrack — A full original score composed for every level and boss encounter. Sounds great with the volume up.  

**Gallery heading:** See it in action  

**Bosses heading:** Meet the Bosses  
**Bosses sub:** They're real. They're enormous. They live at the bottom of the ocean.  
**Boss 1 desc:** Blind. Covered in hair-like filaments. Lives near hydrothermal vents. Flicker's first major problem.  
**Boss 2 desc:** Its jaw unhinges to swallow prey larger than itself. It finds this completely normal.  
**Boss 3 desc:** Fast. Multi-armed. Not interested in negotiating.  
**Boss 4 (mystery) name:** ???  
**Boss 4 (mystery) desc:** What lives at the very bottom of the ocean? You'll find out.  

**Footer studio tagline:** A game by Butterware Studios / Toronto, Canada  
**Footer social heading:** Follow Us  
**Footer store heading:** Get the Game  
**Copyright:** © 2026 Butterware Studios. All rights reserved.  

---

*End of specification.*  
*Butterware Studios | Flicker Website v2 | May 2026*
