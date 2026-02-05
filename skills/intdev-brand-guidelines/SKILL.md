---
name: intdev-brand-guidelines
description: Apply Internet Development Studio Company (INTDEV) brand identity including Server Mono typography, brand colors, CSS custom properties, theme system, and SVG logos. Use when building or styling websites, applications, or artifacts that should follow INTDEV's visual identity.
license: MIT
metadata:
  author: internet-development
  version: "1.0"
---

# INTDEV Brand Guidelines

## Overview

The Internet Development Studio Company (INTDEV) has a distinctive visual identity built around monospace typography, precise spacing, and a multi-theme color system. This skill covers Server Mono font setup, the complete CSS custom property system, theme variants, and logo usage.

**Keywords**: branding, visual identity, Server Mono, typography, colors, themes, CSS variables, INTDEV, internet.dev

## Server Mono

Server Mono is INTDEV's signature typeface — a monospace font inspired by typewriters, Apple's San Francisco Mono, ASCII art, and command-line interfaces. Released in 2024 under the SIL Open Font License 1.1.

- **Repository**: [internet-development/www-server-mono](https://github.com/internet-development/www-server-mono)
- **Install locally**: `brew install --cask font-server-mono`
- **CDN**: jsDelivr (see below)

### CDN Setup (Recommended)

Add to your HTML `<head>`:

```html
<link rel="preconnect" href="https://cdn.jsdelivr.net">
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/internet-development/www-server-mono@latest/server-mono.css">
```

### Self-Hosted Setup

Download font files from [GitHub Releases](https://github.com/internet-development/www-server-mono/releases) and add to your CSS:

```css
@font-face {
  font-family: 'ServerMono';
  src: url('/fonts/ServerMono-Regular.woff2') format('woff2'),
       url('/fonts/ServerMono-Regular.woff') format('woff'),
       url('/fonts/ServerMono-Regular.otf') format('opentype');
  font-weight: normal;
  font-style: normal;
  font-display: swap;
}

@font-face {
  font-family: 'ServerMono';
  src: url('/fonts/ServerMono-RegularOblique.woff2') format('woff2'),
       url('/fonts/ServerMono-RegularOblique.woff') format('woff'),
       url('/fonts/ServerMono-RegularOblique.otf') format('opentype');
  font-weight: normal;
  font-style: oblique;
  font-display: swap;
}
```

### Font Family Variables

INTDEV projects use these CSS custom properties for font families:

```css
--font-family: -apple-system, BlinkMacSystemFont, helvetica neue, helvetica, sans-serif;
--font-family-mono: 'ServerMono', Consolas, monaco, monospace;
--font-family-serif: Georgia, Times New Roman, serif;
```

Server Mono is the primary mono font and is used for code, terminal UI, and the Sacred Computer (SRCL) component library.

## Color System

INTDEV uses a comprehensive CSS custom property color system. All colors are defined as `rgba()` values with optional alpha variants.

### Core Palette

**Grayscale**:
- `--color-black-100`: `rgba(0, 0, 0, 1)` — True black
- `--color-gray-100`: `rgba(22, 22, 22, 1)` — Near black
- `--color-gray-90`: `rgba(38, 38, 38, 1)`
- `--color-gray-80`: `rgba(57, 57, 57, 1)`
- `--color-gray-70`: `rgba(82, 82, 82, 1)`
- `--color-gray-60`: `rgba(111, 111, 111, 1)`
- `--color-gray-50`: `rgba(141, 141, 141, 1)`
- `--color-gray-40`: `rgba(168, 168, 168, 1)`
- `--color-gray-30`: `rgba(198, 198, 198, 1)`
- `--color-gray-20`: `rgba(224, 224, 224, 1)`
- `--color-gray-10`: `rgba(244, 244, 244, 1)`
- `--color-white`: `rgba(255, 255, 255, 1)` — True white

**Accent Colors**:
- `--color-blue-60`: `rgba(15, 98, 254, 1)` — Primary blue
- `--color-red-60`: `rgba(218, 30, 40, 1)` — Error red
- `--color-green-60`: `rgba(25, 128, 56, 1)` — Success green
- `--color-gold-30`: `rgba(241, 194, 27, 1)` — Gold accent

**Specialty Palettes** (for themes):
- Daybreak: warm amber-orange range (`--color-daybreak` through `--color-daybreak-100`)
- Neon Green: terminal green range (`--color-neon-green-70` through `--color-neon-green-100`)
- Blue: deep blue range (`--color-blue-80` through `--color-blue-10`)

### Type Scale

```css
--type-scale-1: 3.815rem;
--type-scale-2: 3.052rem;
--type-scale-3: 2.441rem;
--type-scale-4: 1.953rem;
--type-scale-5: 1.563rem;
--type-scale-6: 1.25rem;
--type-scale-7: 1rem;

--type-scale-fixed-large: 20px;
--type-scale-fixed-medium: 16px;
--type-scale-fixed-small: 14px;
--type-scale-fixed-tiny: 12px;
--type-scale-fixed-label: 10px;
```

## Theme System

INTDEV projects support multiple themes applied via body class. Each theme sets semantic `--theme-*` variables that components consume.

### Available Themes

| Body Class | Description |
|------------|-------------|
| `theme-light` | Light background, dark text. Default for most sites. |
| `theme-dark` | Dark background, light text. Uses gold accent. |
| `theme-daybreak` | Deep amber/orange theme. Warm and distinctive. |
| `theme-blue` | Deep blue background. Uses gold accent. |
| `theme-neon-green` | Terminal green on dark. Retro CRT aesthetic. |

### Theme Variables

Every theme defines these semantic variables:

```css
--theme-background          /* Page background */
--theme-background-overlay  /* Overlay background (40% opacity) */
--theme-foreground          /* Subtle foreground (10% opacity) */
--theme-foreground-secondary /* Secondary foreground (20% opacity) */
--theme-text                /* Primary text color */
--theme-border              /* Default border color */
--theme-border-subdued      /* Subtle border */
--theme-button              /* Button background */
--theme-button-text         /* Button text */
--theme-primary             /* Primary accent */
--theme-input-active        /* Active input highlight */
--theme-success             /* Success state */
--theme-error               /* Error state */
--theme-box-shadow-modal    /* Modal shadow */
--theme-box-shadow-button   /* Button shadow */
--theme-box-shadow-button-hover /* Button hover shadow */
```

### Example: Light Theme Values

```css
body.theme-light {
  --theme-background: var(--color-white);
  --theme-text: var(--color-black-100);
  --theme-border: var(--color-gray-20);
  --theme-button: var(--color-black-100);
  --theme-button-text: var(--color-white);
  --theme-primary: var(--color-blue-60);
}
```

### Example: Dark Theme Values

```css
body.theme-dark {
  --theme-background: var(--color-black-100);
  --theme-text: var(--color-white);
  --theme-border: var(--color-gray-90);
  --theme-button: var(--color-white);
  --theme-button-text: var(--color-black-100);
  --theme-primary: var(--color-gold-30);
}
```

## Logos

INTDEV has three SVG logo variants. All are available at [internet.dev](https://internet.dev):

1. **Logomark only** — The INTDEV symbol without text
2. **Event badge** — For when hosting events at the studio
3. **Full lockup** — Symbol + "INTDEV" brand name

When using logos, follow these rules:
- Always use SVG format for web
- Ensure sufficient contrast against the background
- Do not modify the logo proportions or colors
- Use the appropriate variant for the context

## Base Styles

INTDEV projects apply a comprehensive CSS reset and use these base conventions:

- `box-sizing: border-box` on all elements
- `font-variant-numeric: tabular-nums` for consistent number widths
- Base font size: `16px` (scales to `12px` on mobile via `@media (max-width: 768px)`)
- Font family: system sans-serif stack by default, Server Mono for monospace contexts
- All elements have `margin: 0; padding: 0; border: 0; vertical-align: baseline`
