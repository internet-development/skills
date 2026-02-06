---
name: nextjs-sass-base
description: Scaffold minimal web projects using INTDEV's nextjs-sass-base template — the lightest possible Next.js + SASS + TypeScript starting point with just the essentials. Use when you want a clean slate without the demos, design system components, or d3 dependencies of the full nextjs-sass-starter.
license: MIT
metadata:
  author: internet-development
  version: "1.0"
---

# nextjs-sass-base

## Overview

The nextjs-sass-base is the minimal version of INTDEV's project template. Where `nextjs-sass-starter` comes loaded with 60+ demos, a full design system, and d3 charting, `nextjs-sass-base` gives you only the bare essentials — just enough structure to start building immediately without deleting boilerplate.

- **Repository**: [internet-development/nextjs-sass-base](https://github.com/internet-development/nextjs-sass-base)
- **Stack**: Next.js 16, React 19, TypeScript, SASS
- **When to use**: New projects where you want a clean slate, quick prototypes, or when the full starter has more than you need

## Quick Start

### From Template

1. Go to [internet-development/nextjs-sass-base](https://github.com/internet-development/nextjs-sass-base) and click **Use this template**
2. Clone your new repository
3. Install and run:

```bash
npm install
npm run dev
```

4. Open `http://localhost:10000`

### From Scratch

```bash
git clone https://github.com/internet-development/nextjs-sass-base.git my-project
cd my-project
rm -rf .git
git init
npm install
npm run dev
```

## Project Structure

```
nextjs-sass-base/
├── app/                    # Next.js App Router (layout, metadata)
├── pages/                  # Next.js Pages Router (routes)
│   ├── _app.tsx            # App wrapper with Providers
│   ├── _document.tsx       # HTML document structure
│   ├── oauth.tsx           # OAuth callback page
│   └── api/                # API routes directory
├── components/             # Minimal component set
│   ├── DefaultLayout.tsx   # Standard page layout wrapper
│   ├── DefaultLayout.module.scss
│   ├── DefaultMetaTags.tsx # SEO meta tags
│   ├── ModalContext.tsx    # Modal state management context
│   ├── Page.tsx            # Page wrapper component
│   └── Providers.tsx       # React context providers
├── common/                 # Shared utilities
├── modules/                # Shared SCSS mixins
├── public/                 # Static assets
├── global.scss             # Global styles, CSS reset, variables, themes
├── animations.scss         # CSS animation keyframes
├── package.json
├── next.config.js
└── tsconfig.json
```

## How It Differs from nextjs-sass-starter

| Feature | nextjs-sass-base | nextjs-sass-starter |
|---------|-----------------|---------------------|
| Components | 6 essential files | 11+ components |
| Pages | Index + OAuth | 60+ demo pages |
| Design system (`system/`) | None | Full system (buttons, forms, charts, etc.) |
| Demo pages (`demos/`) | None | 60+ demos |
| d3 dependency | No | Yes |
| js-cookie dependency | No | No |
| Total dependencies | 4 (next, react, react-dom, sass) | 6 |
| Next.js version | 16 | 15 |
| Purpose | Clean starting point | Reference implementation |

## Key Conventions

### Same Conventions as the Full Starter

The base template follows all the same INTDEV conventions:

- **Port 10000** — Dev and production server on port `10000` for Render.com compatibility
- **SASS CSS Modules** — Component styles in `.module.scss` files
- **TypeScript** — All source files are TypeScript
- **App Router + Pages Router** — App Router for layout, Pages Router for routes
- **Server Mono** — Font declarations in `global.scss`
- **Theme system** — Full `theme-light`, `theme-dark`, `theme-daybreak`, `theme-blue`, `theme-neon-green` support
- **CSS custom properties** — Complete color, typography, and theme variable system in `global.scss`

### Dependencies

Absolute minimum — just Next.js, React, and SASS:

```json
{
  "dependencies": {
    "next": "^16.0.7",
    "react": "^19.2.0",
    "react-dom": "^19.2.0",
    "sass": "1.94.2"
  }
}
```

### Included Components

The 6 included component files give you the bare minimum to build pages:

| Component | Purpose |
|-----------|---------|
| `DefaultLayout` | Page wrapper with standard HTML structure and styles |
| `DefaultMetaTags` | `<Head>` component with standard meta tags |
| `ModalContext` | React context for modal state management |
| `Page` | Page-level wrapper component |
| `Providers` | React context providers wrapper |

### Adding a Page

Create a new file in `pages/`:

```tsx
import DefaultLayout from '@/components/DefaultLayout';

export default function MyPage() {
  return (
    <DefaultLayout>
      <h1>Hello World</h1>
      <p>Your content here</p>
    </DefaultLayout>
  );
}
```

### Adding Components

Since the base template has no design system components, you have two paths:

1. **Copy from SRCL** — Browse [sacred.computer](https://sacred.computer), find components you need, copy the `.tsx` + `.module.scss` files into your `components/` directory

2. **Copy from nextjs-sass-starter** — Browse [wireframes.internet.dev](https://wireframes.internet.dev), copy components from the `system/` directory of that repo

3. **Build your own** — Create `ComponentName.tsx` + `ComponentName.module.scss` following the CSS Modules pattern

## When to Choose Which Template

| Scenario | Use |
|----------|-----|
| Starting a new client project from scratch | `nextjs-sass-base` |
| Learning INTDEV patterns / exploring components | `nextjs-sass-starter` |
| Need auth + payments pre-wired | `nextjs-intdev-services-auth-payments` |
| Building a component-rich application | `nextjs-sass-starter` |
| Quick prototype or landing page | `nextjs-sass-base` |
| Need data visualization | `nextjs-sass-starter` (has d3) |

## Related

- [nextjs-sass-starter](https://github.com/internet-development/nextjs-sass-starter) — Full template with 60+ demos and complete design system
- [nextjs-intdev-services-auth-payments](https://github.com/internet-development/nextjs-intdev-services-auth-payments) — Template with auth, Stripe payments, and user tiers
- [www-sacred](https://github.com/internet-development/www-sacred) — SRCL component library to copy components from
