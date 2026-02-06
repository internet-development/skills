---
name: server-mono
description: Set up and use Server Mono, INTDEV's open-source monospace typeface. Covers all installation methods — Homebrew, CDN via jsDelivr, self-hosted font files, and npm-style CSS import — plus usage patterns for web, desktop, and terminal applications.
license: MIT
metadata:
  author: internet-development
  version: "1.0"
---

# Server Mono

## Overview

Server Mono is a monospace typeface created by the Internet Development Studio Company. Inspired by typewriters, Apple's San Francisco Mono, ASCII art, command-line interfaces, and programming tools, it offers excellent readability and pairs well with its uniform, predictable, and orderly appearance.

- **Website**: [servermono.com](https://servermono.com)
- **Repository**: [internet-development/www-server-mono](https://github.com/internet-development/www-server-mono)
- **License**: SIL Open Font License 1.1
- **Designers**: Tim Vanhille and Matthieu Salvaggio, with direction from Jimmy Lee and the INTDEV community
- **Released**: 2024

## Font Files

Server Mono ships as a single-weight font with a regular and oblique variant:

| File | Format | Best For |
|------|--------|----------|
| `ServerMono-Regular.woff2` | WOFF2 | Web (best compression, modern browsers) |
| `ServerMono-Regular.woff` | WOFF | Web (good compression, wider support) |
| `ServerMono-Regular.otf` | OpenType | Desktop apps, print, universal support |
| `ServerMono-RegularOblique.woff2` | WOFF2 | Web italic/oblique |
| `ServerMono-RegularOblique.woff` | WOFF | Web italic/oblique |
| `ServerMono-RegularOblique.otf` | OpenType | Desktop italic/oblique |

The source `.glyphs` file is also available in the repository at `fonts/ServerMono.glyphs`.

## Installation Methods

### 1. Homebrew (macOS — Local Install)

Install Server Mono system-wide on macOS:

```bash
brew install --cask font-server-mono
```

After installation, Server Mono is available in all macOS applications — terminals, text editors, IDEs, design tools, etc.

### 2. CDN via jsDelivr (Web — Zero Config)

The fastest way to add Server Mono to a website. Add to your HTML `<head>`:

```html
<link rel="preconnect" href="https://cdn.jsdelivr.net">
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/internet-development/www-server-mono@latest/server-mono.css">
```

This loads a pre-built CSS file that declares both the regular and oblique `@font-face` rules. No font files to download or host.

### 3. Self-Hosted (Web — Full Control)

Download the font files from [GitHub Releases](https://github.com/internet-development/www-server-mono/releases) and add them to your project's public/static directory.

Then add the `@font-face` declarations to your CSS:

```css
/* Regular weight */
@font-face {
  font-family: 'ServerMono';
  src: url('/fonts/ServerMono-Regular.woff2') format('woff2'),
       url('/fonts/ServerMono-Regular.woff') format('woff'),
       url('/fonts/ServerMono-Regular.otf') format('opentype');
  font-weight: normal;
  font-style: normal;
  font-display: swap;
}

/* Oblique variant */
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

Adjust the URL paths to match your project structure. The examples above assume font files are in a `/fonts/` directory relative to your site root.

### 4. CDN Direct Links (Web — Custom CSS)

If you want to write your own `@font-face` rules but host nothing, use the jsDelivr URLs directly:

```css
@font-face {
  font-family: 'ServerMono';
  src: url('https://cdn.jsdelivr.net/gh/internet-development/www-server-mono@latest/public/fonts/ServerMono-Regular.woff2') format('woff2'),
       url('https://cdn.jsdelivr.net/gh/internet-development/www-server-mono@latest/public/fonts/ServerMono-Regular.woff') format('woff'),
       url('https://cdn.jsdelivr.net/gh/internet-development/www-server-mono@latest/public/fonts/ServerMono-Regular.otf') format('opentype');
  font-weight: normal;
  font-style: normal;
  font-display: swap;
}

@font-face {
  font-family: 'ServerMono';
  src: url('https://cdn.jsdelivr.net/gh/internet-development/www-server-mono@latest/public/fonts/ServerMono-RegularOblique.woff2') format('woff2'),
       url('https://cdn.jsdelivr.net/gh/internet-development/www-server-mono@latest/public/fonts/ServerMono-RegularOblique.woff') format('woff'),
       url('https://cdn.jsdelivr.net/gh/internet-development/www-server-mono@latest/public/fonts/ServerMono-RegularOblique.otf') format('opentype');
  font-weight: normal;
  font-style: oblique;
  font-display: swap;
}
```

### 5. INTDEV S3 (Internal Projects)

INTDEV projects hosted on the INTDEV infrastructure can also load from the S3 bucket. This is what `nextjs-sass-starter` uses in its `global.scss`:

```css
@font-face {
  font-family: 'ServerMono';
  src: url('https://intdev-global.s3.us-west-2.amazonaws.com/public/internet-dev/25071f6e-4cc8-4f91-8387-e4c60b9231de.woff2') format('woff2'),
       url('https://intdev-global.s3.us-west-2.amazonaws.com/public/internet-dev/2bddcba4-a541-4af6-b4b6-5dfb1e4875f5.woff') format('woff'),
       url('https://intdev-global.s3.us-west-2.amazonaws.com/public/internet-dev/45c36a19-7078-4880-89a5-2c700a28070a.otf') format('opentype');
  font-weight: normal;
  font-style: normal;
}
```

For new projects, prefer the jsDelivr CDN or self-hosted approach instead.

## Using Server Mono

### As the site-wide font

```css
:root {
  font-family: 'ServerMono', monospace;
}
```

### As the monospace font (INTDEV convention)

INTDEV projects use Server Mono alongside a system sans-serif stack:

```css
html, body {
  --font-family: -apple-system, BlinkMacSystemFont, helvetica neue, helvetica, sans-serif;
  --font-family-mono: 'ServerMono', Consolas, monaco, monospace;
  --font-family-serif: Georgia, Times New Roman, serif;

  font-family: var(--font-family);
}

code, pre, .monospace {
  font-family: var(--font-family-mono);
}
```

### Oblique / italic text

To use the oblique variant, set `font-style` to `oblique` or `italic`:

```css
em, .italic {
  font-family: 'ServerMono', monospace;
  font-style: oblique;
}
```

### In a Next.js project

If you're using `nextjs-sass-starter` or `nextjs-sass-base`, Server Mono is already declared in `global.scss`. Just use the CSS variable:

```scss
.myComponent {
  font-family: var(--font-family-mono);
}
```

### Terminal / IDE Setup

After installing via Homebrew (`brew install --cask font-server-mono`):

- **VS Code**: Settings → `"editor.fontFamily": "'ServerMono', Menlo, Monaco, monospace"`
- **iTerm2**: Profiles → Text → Font → Server Mono
- **Terminal.app**: Preferences → Profiles → Font → Server Mono
- **Cursor**: Settings → `"editor.fontFamily": "'ServerMono', monospace"`

## Design Characteristics

- **Single weight** — One weight, clean and uniform
- **Monospace** — Fixed-width characters for perfect alignment
- **Character set** — Full Latin alphabet, numbers, symbols, and punctuation
- **Line height** — Designed for comfortable reading at standard line heights
- **Pairing** — Pairs well with system sans-serif fonts (the INTDEV convention) or other clean sans-serifs

## Projects Using Server Mono

- [sacred.computer](https://sacred.computer) — SRCL component library
- [internet.dev](https://internet.dev) — INTDEV website
- [txt.dev](https://txt.dev) — Writing platform
- [users.garden](https://users.garden) — Account management
- [beautifulthings.xyz](https://beautifulthings.xyz) — Visual showcase
- [servermono.com](https://servermono.com) — Font showcase site
