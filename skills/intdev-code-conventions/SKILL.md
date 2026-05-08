---
name: intdev-code-conventions
description: Write code following Internet Development Studio Company (INTDEV) conventions — commenting, file organization, component architecture, CSS patterns, React idioms, TypeScript config, API patterns, and tooling. Use when writing or reviewing code in any INTDEV project.
license: MIT
metadata:
  author: internet-development
  version: "1.0"
---

# INTDEV Code Conventions

## Overview

This skill teaches agents how to write code the way Internet Development Studio Company (INTDEV) does across all repositories. These conventions are consistent across every INTDEV project — from [Sacred Computer (SRCL)](https://sacred.computer) to the [API](https://github.com/internet-development/apis) to [Daedalus](https://github.com/internet-development/daedalus).

**Organization**: [internet-development](https://github.com/internet-development) on GitHub

## Core Principles

1. **Minimal dependencies** — Vendor code in `modules/` rather than adding npm packages. Use built-in utilities from `common/utilities.ts` over npm equivalents like `clsx`, `classnames`, `lodash`, or `date-fns`.

2. **No unnecessary abstraction** — Function declarations, not arrow functions. Props spreading, not verbose interfaces. Inline styles for one-off spacing, not new CSS classes.

3. **Consistency over cleverness** — Same Prettier config, same port (`10000` frontend, `10001` API), same file patterns, same import style across every repo.

4. **Build is the gate** — No linter. `next build` typechecks the code. That's it.

5. **Terminal aesthetic** — Server Mono, monospace grids, precise spacing in multiples of 4.

## Quick Reference

These are the conventions agents must follow immediately. Load reference files for deeper context.

### Commenting

```typescript
// NOTE(@jimmylee): Explanation of WHY, not WHAT.
// TODO(@caidanw): Planned work with owner attribution.
```

No self-documenting comments. No commenting what code does — only why.

See [references/commenting.md](references/commenting.md) for full patterns.

### Imports

```typescript
import styles from './Component.module.css';

import * as React from 'react';

import * as Constants from '@common/constants';
import * as Utilities from '@common/utilities';

import Button from '@components/Button';
```

Always namespace imports (`import * as X`) for React and utility modules. Never destructure.

See [references/file-organization.md](references/file-organization.md) for import ordering and path aliases.

### Components

```typescript
export default function Button(props) {
  if (props.href) {
    return <a className={styles.root} {...props} />;
  }
  return <button className={styles.root} {...props}>{props.children}</button>;
}
```

Function declarations. Props spreading. No arrow functions. No Props interfaces unless the file already has them. Anchor-or-button polymorphism when `props.href` is present.

See [references/react-patterns.md](references/react-patterns.md) for all React conventions.

### CSS

```css
.root {
  display: flex;
  align-items: center;
  min-height: 48px;
  padding: 4px 24px;
  border-radius: 8px;
  background: var(--theme-button);
  color: var(--theme-button-text);
  transition: 200ms ease all;
}
```

Vanilla CSS Modules (`.module.css`). `.root` as outer class. Theme tokens via `var(--theme-*)`. No Tailwind, no CSS-in-JS, no SCSS in new projects.

See [references/css-conventions.md](references/css-conventions.md) for spacing, typography, themes, and precision values.

### File Structure

```
components/
  Button.tsx
  Button.module.css
common/
  utilities.ts
  constants.ts
modules/
  cookies/index.ts    # vendored, zero-dep
```

Colocated `.tsx` + `.module.css`. Path aliases via tsconfig. Vendored code in `modules/`.

See [references/file-organization.md](references/file-organization.md) and [references/component-tiers.md](references/component-tiers.md).

### Prettier

```json
{
  "bracketSpacing": true,
  "printWidth": 9999,
  "semi": true,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "es5"
}
```

`printWidth: 9999` is intentional. Long lines are expected. No line wrapping.

See [references/tooling.md](references/tooling.md) for the full config and build conventions.

## Reference Files

Load these for deeper context on specific areas:

| Reference | When to load |
|-----------|-------------|
| [commenting.md](references/commenting.md) | Writing or reviewing comments |
| [file-organization.md](references/file-organization.md) | Creating files, setting up imports, path aliases |
| [component-tiers.md](references/component-tiers.md) | Building components, deciding where a component lives |
| [css-conventions.md](references/css-conventions.md) | Writing styles, working with themes, spacing, typography |
| [react-patterns.md](references/react-patterns.md) | Writing React components, hooks, data fetching |
| [typescript-config.md](references/typescript-config.md) | Setting up tsconfig, understanding strictness levels |
| [api-patterns.md](references/api-patterns.md) | Writing API routes, response shapes, validation |
| [tooling.md](references/tooling.md) | Prettier, build config, testing, vendored modules |
