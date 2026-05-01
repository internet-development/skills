# CSS Conventions

## CSS Modules

All styles use vanilla CSS Modules (`.module.css`). No Tailwind, no CSS-in-JS, no SCSS in new projects.

```css
/* Button.module.css */
.root {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 48px;
  padding: 4px 24px;
  border-radius: 8px;
  background: var(--theme-button);
  color: var(--theme-button-text);
  transition: 200ms ease all;
  cursor: pointer;
}
```

```tsx
import styles from './Button.module.css';

export default function Button(props) {
  return <button className={styles.root} {...props} />;
}
```

Some older repos use `.module.scss` — follow whatever the existing project uses, but new projects use `.module.css` with native CSS nesting.

## `.root` Convention

The outermost class in every CSS Module is `.root`. Variants and child elements are flat sibling classes, not nested modifiers:

```css
/* GOOD */
.root { ... }
.visual { ... }
.loader { ... }
.left { ... }
.right { ... }
.stretch { ... }
.item { ... }

/* BAD — don't use BEM or nested modifier classes */
.root { ... }
.root--large { ... }
.root__icon { ... }
```

## Theme Tokens

Always use semantic theme tokens. Never hardcode colors.

```css
/* GOOD */
color: var(--theme-text);
background: var(--theme-background);
border: 1px solid var(--theme-border);

/* BAD */
color: #000;
background: white;
border: 1px solid #e0e0e0;
```

### Semantic Variables

Every theme defines these variables:

| Variable | Purpose |
|----------|---------|
| `--theme-background` | Page background |
| `--theme-background-overlay` | Overlay background (40% opacity) |
| `--theme-foreground` | Subtle foreground (10% opacity) |
| `--theme-foreground-secondary` | Secondary foreground (20% opacity) |
| `--theme-text` | Primary text color |
| `--theme-border` | Default border |
| `--theme-border-subdued` | Subtle border |
| `--theme-button` | Button background |
| `--theme-button-text` | Button text |
| `--theme-primary` | Primary accent |
| `--theme-input-active` | Active input highlight |
| `--theme-success` | Success state |
| `--theme-error` | Error state |
| `--theme-box-shadow-modal` | Modal shadow |
| `--theme-box-shadow-button` | Button shadow |
| `--theme-box-shadow-button-hover` | Button hover shadow |

### Five Themes

Applied via body class: `theme-light` (default), `theme-dark`, `theme-daybreak`, `theme-blue`, `theme-neon-green`.

When adding a new theme token, it must be added to **all five** theme blocks in `global.css`.

## Spacing

Multiples of 4: `4, 8, 12, 16, 24, 32, 48, 64`.

For one-off spacing between components, use inline `style` props rather than creating new CSS classes:

```tsx
<InputLabel style={{ marginTop: 24 }}>Label</InputLabel>
<Input style={{ marginTop: 8 }} />
```

## Precision Values

These values are codified. Match them exactly.

| Property | Value |
|----------|-------|
| **Transition** | `200ms ease all` |
| **Breakpoint** | `768px` (Navigation may use `960px`) |
| **Button height** | `min-height: 48px` |
| **Button padding** | `4px 24px` |
| **Button radius** | `border-radius: 8px` |
| **Input height** | `height: 48px` |
| **Input padding** | `0 16px` |
| **Input radius** | `border-radius: 4px` |
| **Input focus ring** | `0 0 0 4px var(--theme-input-active)` |
| **Navigation row height** | `48px` |
| **Navigation text** | `text-transform: uppercase; letter-spacing: 0.2px; font-weight: 600` |
| **Navigation side cells** | `min-width: 240px` |
| **Content max-width** | `AppLayout: 768px`, `ThinAppLayout: 512px` |
| **Layout height** | `min-height: calc(100dvh - 48px)` |

## Borders

Two approaches, both valid:

```css
/* Layout-safe (no layout shift) */
box-shadow: 0 0 0 1px var(--theme-border);

/* Standard */
border: 1px solid var(--theme-border);
```

## Typography

Two scale systems coexist:

**Modular scale** (responsive, `rem` units):
```css
--type-scale-1: 3.815rem;  /* Display */
--type-scale-2: 3.052rem;
--type-scale-3: 2.441rem;
--type-scale-4: 1.953rem;
--type-scale-5: 1.563rem;
--type-scale-6: 1.25rem;
--type-scale-7: 1rem;       /* Body */
```

**Fixed scale** (constant, `px` units — for UI chrome):
```css
--type-scale-fixed-large: 20px;
--type-scale-fixed-medium: 16px;
--type-scale-fixed-small: 14px;
--type-scale-fixed-tiny: 12px;
--type-scale-fixed-label: 10px;
```

Base font size: `16px`, scales to `12px` below `768px`.

Global: `font-variant-numeric: tabular-nums`.

## CSS Reset

Every project includes a comprehensive reset in `global.css`:
- `box-sizing: border-box` on all elements
- `margin: 0; padding: 0; border: 0; vertical-align: baseline` on all elements
- `font-variant-numeric: tabular-nums` globally
- Server Mono loaded via `@font-face` from CDN or S3

## Native CSS Nesting

New projects use native CSS nesting instead of SCSS:

```css
.root {
  display: flex;

  &:hover {
    background: var(--theme-foreground);
  }

  &:focus-visible {
    box-shadow: 0 0 0 4px var(--theme-input-active);
  }
}
```

## `classNames()` Utility

Use the project's `classNames()` from `common/utilities.ts` for conditional classes. Never install `clsx` or `classnames`:

```tsx
import * as Utilities from '@common/utilities';

<div className={Utilities.classNames(styles.root, isActive && styles.active)} />
```
