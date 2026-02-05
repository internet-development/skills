---
name: sacred-computer
description: Build user interfaces with SRCL (Sacred Computer), INTDEV's open-source React component library with terminal aesthetics and monospace character spacing. Use when building UIs that need terminal-style components, monospace layouts, or when working with the Sacred Computer design system.
license: MIT
metadata:
  author: internet-development
  version: "1.0"
---

# Sacred Computer (SRCL)

## Overview

SRCL is an open-source React component and style repository that helps you build web applications, desktop applications, and static websites with terminal aesthetics. Its modular, easy-to-use components emphasize precise monospace character spacing and line heights.

- **Live demo**: [sacred.computer](https://sacred.computer)
- **Repository**: [internet-development/www-sacred](https://github.com/internet-development/www-sacred)
- **Stack**: Next.js, React, TypeScript, SASS (CSS Modules)

## Getting Started

Clone the repository and run locally:

```bash
git clone https://github.com/internet-development/www-sacred.git
cd www-sacred
npm install
npm run dev
```

Visit `http://localhost:10000` to browse all components.

## Architecture

SRCL follows INTDEV's standard project structure:

```
www-sacred/
├── components/          # All SRCL components (TSX + SCSS modules)
├── common/              # Shared utilities and constants
├── modules/             # Shared SCSS mixins and variables
├── pages/               # Next.js pages (component demos)
├── public/              # Static assets
├── global.scss          # Global styles, CSS reset, font-face declarations
├── package.json
└── tsconfig.json
```

### Component Pattern

Every SRCL component follows this pattern:

1. A `.tsx` file exporting a React component
2. A `.module.scss` file with scoped styles
3. All styles use CSS Modules — classes are imported as `styles.className`

```tsx
import styles from './Button.module.scss';

export default function Button({ children, ...props }) {
  return <button className={styles.root} {...props}>{children}</button>;
}
```

## Component Catalog

See [references/components.md](references/components.md) for the complete catalog with descriptions.

### Layout & Structure

| Component | Purpose |
|-----------|---------|
| `Block` | Basic container block |
| `ContentFluid` | Fluid-width content wrapper |
| `Grid` | Grid layout system |
| `Indent` | Indentation wrapper for nested content |
| `Row` | Horizontal row layout |
| `RowSpaceBetween` | Row with space-between alignment |
| `RowEllipsis` | Row with text overflow ellipsis |
| `SidebarLayout` | Sidebar + content layout |

### Navigation & Menus

| Component | Purpose |
|-----------|---------|
| `Navigation` | Top navigation bar |
| `BreadCrumbs` | Breadcrumb navigation trail |
| `ActionBar` | Toolbar with action buttons |
| `ActionButton` | Individual action button |
| `ActionListItem` | Item in an action list |
| `DropdownMenu` | Dropdown menu panel |
| `DropdownMenuTrigger` | Trigger element for dropdown menus |
| `TreeView` | Hierarchical tree navigation |

### Form Controls

| Component | Purpose |
|-----------|---------|
| `Button` | Standard button |
| `ButtonGroup` | Group of related buttons |
| `Checkbox` | Checkbox input |
| `ComboBox` | Searchable select/combo box |
| `DatePicker` | Date selection input |
| `Input` | Text input field |
| `NumberRangeSlider` | Numeric range slider |
| `RadioButton` | Radio button input |
| `RadioButtonGroup` | Group of radio buttons |
| `Select` | Standard select dropdown |
| `TextArea` | Multi-line text input |

### Data Display

| Component | Purpose |
|-----------|---------|
| `DataTable` | Full-featured data table |
| `Table` | Basic table wrapper |
| `TableColumn` | Table column definition |
| `TableRow` | Table row wrapper |
| `Badge` | Status badge / label |
| `Card` | Content card |
| `CardDouble` | Double-width card variant |
| `CodeBlock` | Syntax-highlighted code display |
| `ListItem` | List item |
| `Text` | Text display with monospace styling |

### Feedback & Overlays

| Component | Purpose |
|-----------|---------|
| `AlertBanner` | Alert / notification banner |
| `Dialog` | Modal dialog |
| `Drawer` | Side drawer panel |
| `Message` | Chat-style message bubble |
| `MessageViewer` | Message thread viewer |
| `ModalStack` | Stacked modal system |
| `ModalTrigger` | Trigger element for modals |
| `Popover` | Popover tooltip |
| `Tooltip` | Hover tooltip |

### Loading & Progress

| Component | Purpose |
|-----------|---------|
| `BarLoader` | Horizontal bar loader animation |
| `BarProgress` | Progress bar |
| `BlockLoader` | Block-style loading indicator |
| `MatrixLoader` | Matrix/terminal-style loading animation |

### Visual & Media

| Component | Purpose |
|-----------|---------|
| `Avatar` | User avatar display |
| `Divider` | Horizontal divider |
| `HoverComponentTrigger` | Hover-activated component display |

### Interactive

| Component | Purpose |
|-----------|---------|
| `Accordion` | Expandable/collapsible section |
| `CanvasPlatformer` | Canvas-based platformer game |
| `CanvasSnake` | Canvas-based snake game |
| `Chessboard` | Interactive chessboard |
| `DOMSnake` | DOM-based snake game |

## Design Principles

1. **Monospace first** — All components are designed around Server Mono's character grid. Spacing and sizing align to character widths.

2. **Terminal aesthetic** — Components evoke command-line interfaces, ASCII art, and retro computing while remaining functional and accessible.

3. **CSS Modules** — All styles are scoped via SASS CSS Modules. No global class pollution.

4. **Copy-paste friendly** — Components are designed to be easily copied into your own project. No npm package install required — just copy the `.tsx` and `.module.scss` files.

5. **Minimal dependencies** — SRCL only depends on Next.js, React, and SASS. No additional UI libraries.

## Using SRCL Components in Your Project

Since SRCL is not published as an npm package, the intended workflow is:

1. Browse components at [sacred.computer](https://sacred.computer)
2. Find the component you need
3. Copy the `.tsx` and `.module.scss` files into your project's `components/` directory
4. Import and use the component

Make sure your project has SASS configured and uses the INTDEV font/color variables from `global.scss`. See the [intdev-brand-guidelines](../intdev-brand-guidelines/) skill for the full CSS variable system.
