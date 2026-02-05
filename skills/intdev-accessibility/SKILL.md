---
name: intdev-accessibility
description: Build WCAG 2.1 Level AA compliant web interfaces following INTDEV's documented accessibility approach. Covers semantic HTML, keyboard accessibility, color contrast, alternative text, ARIA landmarks, form error handling, and ADA Title II compliance patterns.
license: MIT
metadata:
  author: internet-development
  version: "1.0"
---

# INTDEV Accessibility

## Overview

INTDEV builds all websites to meet WCAG 2.1 Level AA standards, aligning with the Department of Justice guidelines under Title II of the ADA (effective April 24, 2024, with full compliance required by April 24, 2026). This skill encodes the accessibility patterns and practices used across all INTDEV projects.

**Keywords**: accessibility, WCAG, a11y, ADA, screen reader, keyboard navigation, ARIA, color contrast, semantic HTML

## Core Principles

1. **Semantic HTML first** — Use the right HTML element for the job before reaching for ARIA
2. **Keyboard accessible** — Every interactive element must be reachable and operable via keyboard
3. **Visible focus** — Focus indicators must be clearly visible at all times
4. **Sufficient contrast** — Text meets WCAG AA contrast ratios (4.5:1 normal text, 3:1 large text)
5. **Alternative text** — All non-decorative images have descriptive alt text

## Semantic HTML

### Use Native Elements

| Instead of | Use |
|-----------|-----|
| `<div onClick>` | `<button>` |
| `<div>` for navigation | `<nav>` |
| `<div>` for main content | `<main>` |
| `<div>` for sections | `<section>` with heading |
| `<div>` for lists | `<ul>`, `<ol>`, `<dl>` |
| `<span>` for links | `<a href>` |
| Custom checkbox | `<input type="checkbox">` |

### Document Structure

Every page should have:

```html
<body>
  <header>
    <nav aria-label="Main navigation">...</nav>
  </header>
  <main>
    <h1>Page Title</h1>
    <!-- Content with proper heading hierarchy -->
  </main>
  <footer>...</footer>
</body>
```

### Heading Hierarchy

- Exactly one `<h1>` per page
- Never skip heading levels (h1 → h3)
- Use headings to create a logical document outline

## Keyboard Accessibility

### Focus Management

- All interactive elements must receive focus via Tab key
- Focus order follows visual reading order (left-to-right, top-to-bottom)
- Use `tabindex="0"` to add custom elements to tab order
- Use `tabindex="-1"` for programmatically focusable elements
- Never use `tabindex` values > 0

### Required Keyboard Interactions

| Component | Keys |
|-----------|------|
| Buttons | Enter, Space to activate |
| Links | Enter to follow |
| Checkboxes | Space to toggle |
| Radio buttons | Arrow keys to move, Space to select |
| Dropdowns | Arrow keys to navigate, Enter to select, Escape to close |
| Modals | Escape to close, Tab trapped within modal |
| Menus | Arrow keys to navigate, Enter to select |

### Skip Navigation

Add a skip link as the first focusable element:

```html
<a href="#main-content" class="skip-link">Skip to main content</a>
```

```css
.skip-link {
  position: absolute;
  top: -40px;
  left: 0;
  z-index: 100;
}
.skip-link:focus {
  top: 0;
}
```

## Color & Contrast

### INTDEV Theme Considerations

INTDEV's theme system (`theme-light`, `theme-dark`, `theme-neon-green`, etc.) must maintain sufficient contrast in every theme:

- **Normal text** (< 18pt or < 14pt bold): minimum 4.5:1 contrast ratio
- **Large text** (≥ 18pt or ≥ 14pt bold): minimum 3:1 contrast ratio
- **UI components and graphics**: minimum 3:1 against adjacent colors

### Theme-Specific Checks

| Theme | Background | Text | Check |
|-------|-----------|------|-------|
| `theme-light` | `#ffffff` | `#000000` | 21:1 ✓ |
| `theme-dark` | `#000000` | `#ffffff` | 21:1 ✓ |
| `theme-daybreak` | `#040200` | `#ff6c04` | Verify contrast ≥ 4.5:1 |
| `theme-neon-green` | `#0a2c02` | `#00cf00` | Verify contrast ≥ 4.5:1 |

When using accent colors (`--theme-primary`, `--theme-success`, `--theme-error`), always verify contrast against the current theme background.

### Color Not Sole Indicator

Never use color as the only way to convey information:

- ✅ Error messages with icon + red color + text explanation
- ❌ Red border only to indicate error

## Alternative Text

### Images

```html
<!-- Informative image -->
<img src="photo.jpg" alt="INTDEV team working at Pike Place office" />

<!-- Decorative image -->
<img src="decoration.svg" alt="" role="presentation" />

<!-- Complex image -->
<img src="chart.png" alt="Revenue chart showing 40% growth in Q3" />
<details>
  <summary>Chart data table</summary>
  <table>...</table>
</details>
```

### Icons

```html
<!-- Icon with visible label — hide icon from screen readers -->
<button>
  <svg aria-hidden="true">...</svg>
  <span>Close</span>
</button>

<!-- Icon-only button — provide accessible name -->
<button aria-label="Close dialog">
  <svg aria-hidden="true">...</svg>
</button>
```

## ARIA Landmarks

Use ARIA landmarks to define page regions:

```html
<nav aria-label="Main navigation">...</nav>
<main aria-label="Page content">...</main>
<aside aria-label="Sidebar">...</aside>
<form aria-label="Search">...</form>
```

When using SRCL components, ensure the outer containers have appropriate landmark roles.

## Forms

### Labels

Every form control needs an associated label:

```html
<!-- Visible label (preferred) -->
<label for="email">Email address</label>
<input id="email" type="email" />

<!-- Hidden label (when visual label is not desired) -->
<input type="search" aria-label="Search posts" />
```

### Error Handling

```html
<label for="email">Email address</label>
<input
  id="email"
  type="email"
  aria-invalid="true"
  aria-describedby="email-error"
/>
<p id="email-error" role="alert">Please enter a valid email address</p>
```

### Required Fields

```html
<label for="name">Name <span aria-hidden="true">*</span></label>
<input id="name" type="text" required aria-required="true" />
```

## Dynamic Content

### Live Regions

For content that updates without page reload:

```html
<!-- Polite: announced when user is idle -->
<div aria-live="polite" aria-atomic="true">
  3 results found
</div>

<!-- Assertive: announced immediately (use sparingly) -->
<div aria-live="assertive" role="alert">
  Error: payment failed
</div>
```

### Loading States

```html
<button aria-busy="true" disabled>
  <span class="loader" aria-hidden="true"></span>
  Saving...
</button>
```

## SRCL Component Accessibility Notes

When using Sacred Computer (SRCL) components, keep these in mind:

- **Dialog**: Ensure focus is trapped inside when open, returns to trigger on close
- **DropdownMenu**: Must be keyboard navigable with arrow keys
- **Accordion**: Use `aria-expanded` on trigger, `aria-controls` pointing to content
- **DataTable**: Use proper `<th scope="col">` and `<th scope="row">` headers
- **ModalStack**: Implement focus trap and Escape key handling
- **Navigation**: Wrap in `<nav>` with descriptive `aria-label`

## Testing

### Manual Testing Checklist

1. Tab through entire page — all interactive elements reachable?
2. Activate every control with keyboard only (Enter, Space, Escape, Arrow keys)
3. Verify visible focus indicator on every focused element
4. Test with screen reader (VoiceOver on macOS: Cmd+F5)
5. Zoom to 200% — content still readable and functional?
6. Check color contrast with browser DevTools or axe extension

### Automated Testing

- [axe DevTools](https://www.deque.com/axe/devtools/) browser extension
- [Lighthouse](https://developer.chrome.com/docs/lighthouse/) accessibility audit
- `eslint-plugin-jsx-a11y` for React projects
