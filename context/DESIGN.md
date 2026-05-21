---
name: Bioluminescent Abyssal
colors:
  surface: '#0f1322'
  surface-dim: '#0f1322'
  surface-bright: '#353849'
  surface-container-lowest: '#0a0d1d'
  surface-container-low: '#171b2b'
  surface-container: '#1b1f2f'
  surface-container-high: '#26293a'
  surface-container-highest: '#303445'
  on-surface: '#dfe1f7'
  on-surface-variant: '#e2bdc6'
  inverse-surface: '#dfe1f7'
  inverse-on-surface: '#2c3040'
  outline: '#a98891'
  outline-variant: '#5a4047'
  surface-tint: '#ffb1c8'
  primary: '#ffb1c8'
  on-primary: '#650033'
  primary-container: '#d40072'
  on-primary-container: '#ffebef'
  inverse-primary: '#b90063'
  secondary: '#42e3ce'
  on-secondary: '#003731'
  secondary-container: '#00c6b2'
  on-secondary-container: '#004d44'
  tertiary: '#cdbdff'
  on-tertiary: '#35226c'
  tertiary-container: '#7361ad'
  on-tertiary-container: '#f4edff'
  error: '#ffb4ab'
  on-error: '#690005'
  error-container: '#93000a'
  on-error-container: '#ffdad6'
  primary-fixed: '#ffd9e2'
  primary-fixed-dim: '#ffb1c8'
  on-primary-fixed: '#3e001d'
  on-primary-fixed-variant: '#8e004a'
  secondary-fixed: '#60fae4'
  secondary-fixed-dim: '#39ddc8'
  on-secondary-fixed: '#00201c'
  on-secondary-fixed-variant: '#005047'
  tertiary-fixed: '#e8deff'
  tertiary-fixed-dim: '#cdbdff'
  on-tertiary-fixed: '#1f0756'
  on-tertiary-fixed-variant: '#4c3a84'
  background: '#0f1322'
  on-background: '#dfe1f7'
  surface-variant: '#303445'
  bg-deep: '#050817'
  bg-mid: '#0a0f2c'
  bg-card: '#1e1e2e'
  bg-light: '#f5f4fb'
  text-primary: '#ffffff'
  text-muted: rgba(255, 255, 255, 0.6)
  text-dark: '#0a0f2c'
  border-teal: rgba(0, 200, 180, 0.2)
typography:
  hero-h1:
    fontFamily: Inter
    fontSize: 52px
    fontWeight: '700'
    lineHeight: '1.15'
    letterSpacing: -0.02em
  hero-h1-mobile:
    fontFamily: Inter
    fontSize: 36px
    fontWeight: '700'
    lineHeight: '1.15'
  section-h2:
    fontFamily: Inter
    fontSize: 42px
    fontWeight: '700'
    lineHeight: '1.2'
  section-h2-mobile:
    fontFamily: Inter
    fontSize: 28px
    fontWeight: '700'
    lineHeight: '1.2'
  card-heading:
    fontFamily: Inter
    fontSize: 18px
    fontWeight: '700'
    lineHeight: '1.2'
  body-lg:
    fontFamily: Inter
    fontSize: 18px
    fontWeight: '400'
    lineHeight: '1.7'
  body-sm:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: '400'
    lineHeight: '1.7'
  label-badge:
    fontFamily: Inter
    fontSize: 11px
    fontWeight: '600'
    lineHeight: '1'
    letterSpacing: 2px
  scientific-name:
    fontFamily: Inter
    fontSize: 11px
    fontWeight: '300'
    lineHeight: '1.2'
rounded:
  sm: 0.25rem
  DEFAULT: 0.5rem
  md: 0.75rem
  lg: 1rem
  xl: 1.5rem
  full: 9999px
spacing:
  gutter-desktop: 24px
  gutter-mobile: 16px
  section-padding-v: 80px
  section-padding-v-mobile: 48px
  content-padding-h: 80px
  content-padding-h-mobile: 20px
  gap-cards: 40px
  gap-tiles: 10px
---

## Brand & Style
The design system for this indie deep-sea shoot 'em up captures a "cute but creepy" duality. It is built on a foundation of **Layered Darkness**, simulating the crushing depths of the ocean where light only exists through biological intent. 

The aesthetic leans into a **Modern-Tactile** hybrid with **Bioluminescent** accents. High-contrast neon elements (Teal, Pink, Purple) act as light sources against near-black navy voids, creating a sense of atmospheric pressure and mystery. Motion is central to the brand—elements should feel as though they are floating or pulsing, mimicking the rhythmic drift of marine life.

**Key Visual Principles:**
- **Atmospheric Contrast:** Harsh transitions between deep sea-floor navies and glowing bioluminescent interfaces.
- **Pixel-Perfect Fidelity:** All game assets must utilize `image-rendering: pixelated` to maintain the integrity of the indie art style.
- **Subtle Uncanny Valley:** Balancing soft, friendly pill-shaped buttons with sharp, intense neon glows and unsettling "mystery" content.

## Colors
The palette is a tiered monochromatic navy base punctuated by high-chroma bioluminescent accents.

- **The Deep (Neutrals):** The background hierarchy uses `#050817` for the abyss (base), `#0a0f2c` for secondary surfaces, and `#1e1e2e` for elevated containers like cards. 
- **The Glow (Accents):** 
    - **Pink (#d40072):** Used for primary CTAs and the core brand mark, representing the "heart" or lure.
    - **Teal (#00c8b4):** Used for interactive states, borders, and functional badges. It represents the "safety" of the UI.
    - **Purple (#8c7ac8):** Reserved for scientific or lore-based secondary information.

**Contrast Logic:** On dark backgrounds, use white for primary legibility and 60% white for muted secondary text. When using the `bg-light` section, switch to `text-dark` (#0a0f2c) for headings to maintain a sharp, punchy hierarchy.

## Typography
The system relies exclusively on **Inter** to ground the fantastical game assets in a clean, functional, and highly readable interface.

- **Headlines:** Use Bold (700) weights with tight line-heights and slight negative letter-spacing to feel impactful and "pressurized." 
- **Information Layering:** Section badges use SemiBold (600) with a 2px letter-spacing to create a technical, "scanned" feel. Scientific names for bosses use Light (300) to contrast against the bold boss names.
- **Scaling:** Use fluid scaling for the Hero tagline to ensure the "H1" remains atmospheric across all viewports.

## Layout & Spacing
The layout uses a **Fluid 12-Column Grid** with a max-width of 1440px. 

The rhythm is defined by a high-density vertical stack. Sections are separated by generous padding (80px) to allow the "darkness" to breathe between content areas. 

**Reflow Rules:**
- **Desktop:** Horizontal content padding is 80px. Feature cards are displayed in a 3-column or 4-column row with 40px gaps.
- **Mobile:** Horizontal padding shrinks to 20px. Grid columns collapse into a single-column vertical stack with 16px component gaps.
- **Navigation:** A sticky header with a `blur(12px)` effect requires a `scroll-margin-top` of 80px for all section anchors to prevent content overlap during navigation.

## Elevation & Depth
Depth is communicated through **Tonal Layering** and **Luminescent Glows** rather than physical shadow metaphors.

- **Stacking:** Surfaces move from Deep (#050817) to Mid (#0a0f2c) to Card (#1e1e2e). Higher elevation is always represented by a slightly lighter "ocean" tone.
- **Atmospheric Glows:** Use Teal-tinted shadows (`rgba(0, 200, 180, 0.25)`) only for hover states on gallery tiles to simulate bioluminescent activation.
- **Glassmorphism:** The navigation bar and mobile menus utilize a semi-transparent Mid-Navy with a heavy `backdrop-filter: blur(12px)` to maintain the sense of looking through water.
- **Vignettes:** For "Mystery" or "Boss" cards, apply a radial vignette to draw the eye to the center and darken the edges, enhancing the "creepy" aesthetic.

## Shapes
The shape language is a mix of geometric precision and organic softness.

- **Pill (Full Radius):** Reserved for interactive CTAs and Buttons to provide a "cute" and inviting touch-point.
- **Rounded (16px):** Used for primary containers and cards to keep the UI feeling modern and approachable.
- **Soft (10px - 12px):** Used for internal tiles and image containers to create a slightly sharper, "contained" look for game assets.
- **Badge (6px):** Smallest radius used for labels and technical data points.

## Components

- **Buttons:** Primary buttons must be pill-shaped (`rounded-full`) with a Pink (#d40072) background and white Bold text. On hover, they should scale to `1.03` with a subtle pulse.
- **Cards:** Feature and Boss cards use the `#1e1e2e` background with a `1px solid --color-border-teal`. Hovering over a card transitions the border to solid Teal (#00c8b4).
- **Gallery Tiles:** Use a `10px` radius. On hover, apply a `1.02` scale and a Teal glow (`0 0 16px`).
- **Section Badges:** Small caps, SemiBold, 11px text. Border should be Teal with a `6px` radius.
- **Inputs & Fields:** Should utilize the `#0a0f2c` background with a subtle Teal border. Focus states should trigger a Pink (#d40072) border glow.
- **Motion Principles:** 
    - **Fade-Ups:** All sections should fade in and move up 24px on entry (0.5s duration).
    - **The Lure Pulse:** Any "mystery" elements or key highlight icons should have a 2s infinite opacity loop (0.4 to 1.0) to mimic bioluminescent flickering.