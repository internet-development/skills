---
name: nextjs-sass-starter
description: Scaffold and build web projects using INTDEV's nextjs-sass-starter template — a Next.js + SASS + TypeScript foundation with a complete design system, reusable components, and 60+ demo pages. Use when creating a new website, adding pages or components to an INTDEV project, or working with the nextjs-sass-starter codebase.
license: MIT
metadata:
  author: internet-development
  version: "1.0"
---

# nextjs-sass-starter

## Overview

The nextjs-sass-starter is INTDEV's production template for building websites. It provides a Next.js + TypeScript + SASS foundation with a complete design system, reusable components, and dozens of demos covering everything from authentication to data visualization.

- **Live demo**: [wireframes.internet.dev](https://wireframes.internet.dev)
- **Repository**: [internet-development/nextjs-sass-starter](https://github.com/internet-development/nextjs-sass-starter)
- **Used by**: [internet.dev](https://internet.dev), [sacred.computer](https://sacred.computer), [txt.dev](https://txt.dev), [users.garden](https://users.garden), [servermono.com](https://servermono.com), [beautifulthings.xyz](https://beautifulthings.xyz), and many more

## Quick Start

### From Template

1. Go to [internet-development/nextjs-sass-starter](https://github.com/internet-development/nextjs-sass-starter) and click **Use this template**
2. Clone your new repository
3. Install and run:

```bash
npm install
npm run dev
```

4. Open `http://localhost:10000`

### From Scratch

```bash
git clone https://github.com/internet-development/nextjs-sass-starter.git my-project
cd my-project
npm install
npm run dev
```

**Important**: The dev server runs on port `10000`, not the Next.js default of `3000`. This is for compatibility with [Render.com](https://render.com) deployments.

## Project Structure

```
nextjs-sass-starter/
├── app/                    # Next.js App Router (layout, metadata)
├── pages/                  # Next.js Pages Router (routes)
│   ├── index.tsx           # Homepage
│   └── examples/           # Demo pages organized by category
├── components/             # Reusable React components
│   ├── DefaultLayout.tsx   # Standard page layout wrapper
│   ├── DefaultMetaTags.tsx # SEO meta tags
│   ├── Page.tsx            # Page wrapper component
│   └── Providers.tsx       # React context providers
├── system/                 # Design system primitives
│   ├── animations/         # CSS animation components
│   ├── diagrams/           # Diagram components
│   ├── documents/          # Document templates (invoices, SOWs)
│   ├── forms/              # Form components
│   ├── graphs/             # Data visualization (d3-based)
│   ├── layouts/            # Page layout patterns
│   ├── modals/             # Modal components
│   ├── scroll/             # Scroll-based animations
│   ├── sections/           # Page section patterns
│   ├── svg/                # SVG components and icons
│   ├── testing/            # Testing utilities
│   ├── typography/         # Typography components
│   ├── Button.tsx          # Base button
│   ├── Input.tsx           # Base input
│   ├── Select.tsx          # Base select
│   ├── TextArea.tsx        # Base textarea
│   ├── Navigation.tsx      # Navigation bar
│   ├── Footer.tsx          # Page footer
│   └── Table.tsx           # Data table
├── common/                 # Shared utilities
│   ├── constants.ts        # App-wide constants
│   └── utilities.ts        # Helper functions
├── modules/                # SCSS mixins and shared styles
├── demos/                  # Extended demo page components
├── global.scss             # Global styles, CSS reset, variables, themes
├── animations.scss         # CSS animation keyframes
├── package.json
├── next.config.ts
└── tsconfig.json
```

## Key Conventions

### Stack

- **Next.js 15** with both App Router (for layout) and Pages Router (for routes)
- **TypeScript** for all source files
- **SASS** with CSS Modules for component styles
- **d3** for data visualization
- **Server Mono** as the monospace font

### Dependencies

The template is intentionally minimal:

```json
{
  "dependencies": {
    "d3": "^7.9.0",
    "js-cookie": "^3.0.5",
    "next": "^15.3.3",
    "react": "^19.1.0",
    "react-dom": "^19.1.0",
    "sass": "1.89.1"
  }
}
```

### Styling

- All component styles use **CSS Modules** (`.module.scss` files)
- Global styles, CSS reset, font-face declarations, and the full color/theme variable system live in `global.scss`
- Animation keyframes live in `animations.scss`
- Shared SCSS mixins live in `modules/`
- The theme system supports `theme-light`, `theme-dark`, `theme-daybreak`, `theme-blue`, and `theme-neon-green` via body classes

### Page Creation

To add a new page:

1. Create a new file in `pages/` (e.g., `pages/my-page.tsx`)
2. Wrap content in `<DefaultLayout>` for consistent layout
3. Use components from `system/` and `components/`

```tsx
import DefaultLayout from '@/components/DefaultLayout';
import Navigation from '@/system/Navigation';

export default function MyPage() {
  return (
    <DefaultLayout previewPixelSRC="https://intdev-global.s3.us-west-2.amazonaws.com/template-app-icon.png">
      <Navigation />
      <div>Your content here</div>
    </DefaultLayout>
  );
}
```

### Component Creation

1. Create `ComponentName.tsx` and `ComponentName.module.scss` side by side
2. Import styles as `import styles from './ComponentName.module.scss'`
3. Place in `components/` for app components or `system/` for design system primitives

### Running Scripts

The template supports running standalone scripts:

```bash
npm run script example
```

Scripts live in the project root or a `scripts/` directory and are executed via `ts-node`.

## Demo Categories

The template includes 60+ demo pages at [wireframes.internet.dev](https://wireframes.internet.dev):

| Category | Examples |
|----------|---------|
| **Animations** | Scroll carousels, card flip/tilt, fade, text swapping |
| **Components** | Navigation, dashboards, forms, tables, modals, search UIs, window managers |
| **Features** | Authentication (email, Bluesky, Google, Apple), file uploads (S3/GCS), invoices, threads, settings |
| **System** | Colors, typography, data visualization (12/14 chart types) |
| **Layouts** | Full sections, half sections, horizontal stacks, sidebars |

## Related Templates

- **[nextjs-sass-base](https://github.com/internet-development/nextjs-sass-base)** — Minimal version with less code, for when you want a bare starting point
- **[nextjs-intdev-services-auth-payments](https://github.com/internet-development/nextjs-intdev-services-auth-payments)** — Full template with authentication, payments, and user tiers pre-wired to api.internet.dev
