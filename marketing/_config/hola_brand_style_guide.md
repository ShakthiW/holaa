# holaa — Brand Style Guide

**Status:** Reference document. All values below are pulled directly from
`chatbot-demo-admin/src/app/globals.css` (the live design-token source) and
`docs/holaa.pdf` (the brand mark reference sheet) — this is not a redesign, it's a
transcription of the system already shipping.

---

## 1. Logo & Brand Mark

Per `docs/holaa.pdf`, the brand mark has three approved forms:

1. **Full wordmark:** lowercase `holaa`, where the second letter "o" is replaced by a circular
   smiley-face glyph (closed, laughing `>‿<` eyes, on a lime-green circle). Slightly slanted
   italic cut on select letterforms for rhythm. This is the primary lockup for headers,
   marketing, and the site logo (`public/images/holaa-logo.svg`,
   `public/images/holaa-logo-transparent.svg`).
2. **Smiley mark alone:** the laughing-face glyph on its own, usable as a favicon, app icon, or
   small-scale brand accent when the full wordmark won't fit. Works in two colorways: lime face
   on black background, or black face with lime eyes/mouth on a light background (used as
   `SmileyMark` in-app, e.g. accenting the final-CTA section).
3. **Wave mark:** a separate icon — a stylized waving hand with three curved "sound wave" /
   motion lines trailing from it — used as the hero-section visual anchor
   (`HolaaWaveMark.tsx`). This reads as "hello, greeting, warmth" and pairs with the platform's
   tagline ("Every great stay starts with a holaa").

**Rules:**
- Never recolor the wordmark outside the approved ink/lime/white combinations below.
- Never stretch, skew (beyond the mark's own built-in slant), or add a drop shadow to the
  logotype.
- The smiley glyph replacing the "o" is a fixed part of the mark — never substitute a plain "o"
  in the primary lockup, and never use the smiley glyph as a generic "o" replacement in other
  wordmarks or headlines.
- Maintain clear space around the mark equal to the height of the wordmark's lowercase "h" on
  all sides, minimum.

---

## 2. Color System

### 2.1 Marketing/brand palette (`--holaa-*` tokens, `globals.css`)

| Token | Hex | Usage |
|---|---|---|
| `--holaa-ink` | `#0A0A0A` | Primary text, primary button background, wordmark |
| `--holaa-lime` | `#C1FF72` | Primary accent — CTAs on dark backgrounds, highlight underlines, active states |
| `--holaa-lime-dim` | `#EAFFCF` | Soft accent fill (badges, icon chip backgrounds) |
| `--holaa-paper` | `#FFFFFF` | Page background (marketing site) |
| `--holaa-mist` | `#F5F5F3` | Section background / card background against paper |
| `--holaa-line` | `#E7E7E4` | Hairline borders, dividers |

### 2.2 Dashboard/product palette (light mode)

The dashboard app reuses the same black/lime brand identity but through its own semantic token
set (kept distinct from the marketing tokens because ~60 dashboard files already reference
these variable names):

| Token | Hex | Usage |
|---|---|---|
| `--background` | `#FAFAF9` | App background |
| `--foreground` | `#0A0A0A` | Primary text |
| `--primary` | `#0A0A0A` | Primary buttons/actions |
| `--primary-foreground` | `#C1FF72` | Text/icon on primary-colored surfaces |
| `--accent` / `--holaa-blue-subtle` | `#EAFFCF` | Accent surfaces |
| `--muted-foreground` | `#78716C` | Secondary text |
| `--border` | `#E7E7E4` | Default borders |

**Status colors are deliberately NOT brand lime** — they use conventional semantic colors so
they stay legible as status, distinct from brand accent:

| Status | Foreground | Background |
|---|---|---|
| Success | `#059669` | `#ECFDF5` |
| Warning | `#D97706` | `#FFFBEB` |
| Critical / destructive | `#DC2626` | `#FEF2F2` |

### 2.3 Dark mode (dashboard)

| Token | Hex |
|---|---|
| `--background` | `#0A0A0A` |
| `--foreground` | `#FAFAF9` |
| `--primary` | `#C1FF72` (inverts — lime becomes the primary surface color in dark mode) |
| `--primary-foreground` | `#0A0A0A` |
| `--card` | `#171717` |
| `--accent` | `#2B3A1A` |

**Color usage rule:** lime is an *accent*, never a body-text color and never a large flat
background outside of the inverted dark-mode primary case above — it's most powerful used
sparingly (a CTA button, an underline, a status dot, an icon chip) against black or white.

---

## 3. Typography

Four font families, each with a specific, non-overlapping role (loaded via `next/font/google`
in `src/app/layout.tsx`):

| Font | CSS variable | Role |
|---|---|---|
| **Inter** | `--font-sans` | Default body/UI text, dashboard interface |
| **Manrope** | `--font-alt` | Secondary/alt sans usage where specified |
| **Cormorant Garamond** | `--font-serif` | Editorial serif — used for `.font-serif-title` luxury/editorial headline moments |
| **Plus Jakarta Sans** | `--font-jakarta` → `--font-display` | The **marketing site's actual display/heading font** — every `h1`/`h2`/`h3` on the public marketing pages uses this via the `font-display` utility class |

**Rules:**
- Marketing headlines: `font-display` (Plus Jakarta Sans), bold/extrabold weight,
  tight tracking (`tracking-tight`, letter-spacing ≈ `-0.015em` to `-0.02em`), generous line
  height for large sizes (`leading-[1.05]`–`leading-[1.08]`).
- Body copy: Inter, relaxed line height, `text-[var(--holaa-ink)]/60`–`/80` opacity for
  secondary/supporting text rather than a separate gray color token — this is a deliberate,
  consistent pattern (ink at reduced opacity, not a different hue) for text hierarchy.
- Editorial/luxury emphasis moments only: Cormorant Garamond serif, regular weight, tightened
  tracking — reserve for occasional atmosphere, not default body or headline use.
- Never substitute system fonts for these four in any published material — the font choice is
  load-bearing to the brand's "confident but literary" tone described in
  `hola_brand_voice_guide.md`.

---

## 4. Shape, Spacing & Elevation

- **Corner radius system** is a single base `--radius: 0.75rem` scaled into `sm`/`md`/`lg`/
  `xl`/`2xl`/`3xl`/`4xl` steps (×0.6 through ×2.6). Buttons and pills use full round
  (`rounded-full`); cards typically use `rounded-2xl`–`rounded-3xl`.
- **Card shadow** (`.holaa-card-shadow`): a soft, low-opacity double shadow
  (`0 1px 3px rgba(15,23,42,.04), 0 6px 16px -4px rgba(15,23,42,.02)`) — subtle, never a hard
  drop shadow.
- **Hover lift** (`.holaa-card-hover`): translateY(-2px) plus a slightly stronger shadow on
  hover, `250ms cubic-bezier(0.16, 1, 0.3, 1)` easing — smooth, springy, never abrupt.
- **Buttons:** two canonical styles only —
  - **Primary** (`.btn-holaa-primary`): ink background, lime text, scales to 0.98 on press,
    darkens slightly (`#1A1A1A`) on hover.
  - **Secondary** (`.btn-holaa-secondary`): transparent background, ink border + text, inverts
    to ink-background/lime-text on hover.
  - Both are always full-round (pill-shaped), never square-cornered.

---

## 5. Iconography & Decorative Marks

- **Functional icons:** `lucide-react` throughout — consistent 1.5–2px stroke weight, no mixed
  icon libraries.
- **Decorative brand shapes** (`src/components/ui/Decorations.tsx`): `Blob` (soft organic
  background shape, used at very low opacity behind hero/section content), `Squiggle`
  (hand-drawn-style underline accent beneath emphasized headline words — see the "holaa." and
  "questions nobody asks." examples on the live site), `Sparkle`, `DotGrid`, `SmileyMark` — all
  lime or ink, used sparingly as atmosphere, never as the primary content.
- **The squiggle-underline-on-key-word** pattern is a signature device: pick one word or short
  phrase per major headline to underline this way, not more.

---

## 6. Photography & Imagery Style

Drawn from the actual imagery choices across the live site (Unsplash sourcing, to be replaced
with real property photography per hotel in production use):

- **Golden hour and soft natural light** — sunrise/sunset framing recurs constantly; avoid flat
  midday light or studio lighting.
- **Wide, immersive, slightly cinematic crops** — infinity pools, ocean horizons, private
  villas shot to feel inhabited, not staged.
- **Warm gradient overlays** (`bg-gradient-to-t from-black/60 via-transparent to-transparent`)
  when text sits over a photo — always for legibility, always warm/neutral black, never a
  colored tint.
- **People are implied, rarely posed** — imagery favors place and atmosphere over stock-photo
  smiling models.
- Caption/label chips over images use the lime-on-dark treatment (small uppercase label, e.g.
  "Visual preview") — consistent with the accent-color usage rule in §2.

---

## 7. Motion Principles

Observed in the hero's GSAP sequence (`HeroSection.tsx`) and section reveals
(`staggerReveal`):

- **Entrances are soft and staggered**, never simultaneous — cards/grid items fade + scale in
  with a small stagger (`power2.out` easing), not a hard cut.
- **One signature "personality" animation is allowed per key brand moment** — the wave-mark's
  hand-wave rotation sequence on page load is a deliberate, one-time brand flourish, not a
  repeating idle animation.
- **Respect `prefers-reduced-motion`** — every animated sequence in the codebase checks this
  and skips non-essential motion; this is a hard requirement, not a nice-to-have, for any new
  animated marketing asset.
- **Toggle/tab transitions are fast and functional** (~0.3s, `power2.out`) — motion in UI
  controls (like the pricing billing-cycle toggle) is quick and utilitarian, reserving the
  slower, more expressive easing for one-time entrance moments only.

---

## 8. Applying This System to New Materials (Deck, Social, Ads, etc.)

- Default background: `--holaa-paper` (white) or `--holaa-ink` (black) — the brand reads best
  in high contrast; avoid mid-tone gray backgrounds.
- Default accent: `--holaa-lime` used sparingly (one CTA, one highlight, one icon chip per
  screen/slide) — resist the temptation to lime-wash a whole layout.
- Default type pairing: Plus Jakarta Sans (display/headline) + Inter (body) covers the large
  majority of marketing use cases; reserve Cormorant Garamond for a single luxury/editorial
  accent moment per piece, if at all.
- Default shape language: full-round pills for actions, large soft-radius cards for content
  blocks, one soft decorative Blob/Squiggle accent per section — not per element.

---

## 9. Related Documents

- **[[hola_brand_context]]** — the "why" behind this visual system
- **[[hola_brand_voice_guide]]** — the words that go inside this system
- **[[hola_product_offerings]]** — what this system is dressing up
