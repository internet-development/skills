# React Patterns

## Component Declaration

Always function declarations. Never arrow functions. No explicit Props interface unless the file already has one.

```typescript
// GOOD
export default function Button(props) {
  return <button className={styles.root} {...props}>{props.children}</button>;
}

// BAD — arrow function
const Button = (props) => { ... };

// BAD — explicit Props interface (unless file already uses them)
interface ButtonProps {
  children: React.ReactNode;
  onClick?: () => void;
}
export default function Button({ children, onClick }: ButtonProps) { ... }
```

Props are spread onto the underlying element. This keeps components flexible without verbose interface definitions.

## React Import

Always namespace import. Never destructure.

```typescript
// GOOD
import * as React from 'react';

const [value, setValue] = React.useState('');
const ref = React.useRef(null);
const memoized = React.useMemo(() => compute(), [dep]);

// BAD
import React, { useState, useRef, useMemo } from 'react';
import { useState } from 'react';
```

## Namespace Imports for Utilities

Same pattern extends to all common/utility modules:

```typescript
import * as Constants from '@common/constants';
import * as Utilities from '@common/utilities';
import * as Server from '@common/server';
import * as Query from '@data/query';

// Usage
Utilities.classNames(styles.root, styles.active);
Utilities.isEmpty(value);
Constants.API_URL;
```

## Anchor-or-Button Polymorphism

Components that can be links or buttons switch element based on `props.href`:

```typescript
export default function Button(props) {
  if (props.href) {
    return <a className={styles.root} {...props} />;
  }
  return <button className={styles.root} {...props}>{props.children}</button>;
}
```

This pattern is used in `Button`, `SmallButton`, `Text`, `P`, `SubText`, and similar components.

## Inline Style for Spacing

One-off spacing between components uses inline `style` props. Don't create CSS classes for spacing:

```tsx
// GOOD
<InputLabel style={{ marginTop: 24 }}>Email</InputLabel>
<Input style={{ marginTop: 8 }} placeholder="you@example.com" />
<Button style={{ marginTop: 16 }}>Submit</Button>

// BAD — don't create classes just for margin
<InputLabel className={styles.labelSpacing}>Email</InputLabel>
```

## Built-In Utilities Over npm Packages

`common/utilities.ts` provides these. Use them instead of npm equivalents:

| Utility | Use instead of |
|---------|---------------|
| `Utilities.classNames()` | `clsx`, `classnames` |
| `Utilities.isEmpty()` | Manual null/undefined/empty checks |
| `Utilities.debounce()` | `lodash.debounce` |
| `Utilities.formatDollars()` | `Intl.NumberFormat` boilerplate |
| `Utilities.timeAgo()` | `date-fns`, `moment` |
| `Utilities.createSlug()` | `slugify` |
| `Utilities.bytesToSize()` | `filesize` |
| `Utilities.elide()` | Manual string truncation |
| `Utilities.noop` | Inline `() => {}` |

## Data Fetching

Centralized `getData()` helper in `common/queries.ts`. No React Query, no SWR, no TanStack.

```typescript
// common/queries.ts
export async function getData({ route, key, body }, qualifier = 'data') {
  const response = await fetch(route, {
    method: 'POST',
    headers: { 'X-API-KEY': key, 'Content-Type': 'application/json' },
    body: JSON.stringify(body),
  });
  const result = await response.json();
  if (!result) return null;
  return result[qualifier];
}
```

Individual queries are thin wrappers:

```typescript
export async function getUser({ key }) {
  return await getData({ route: `${API_URL}/api/users/viewer`, key, body: {} });
}
```

## SVG Icons

Icons are inline React components, not imported SVG files:

```typescript
// elements/icons/IconArrow.tsx
export default function IconArrow(props) {
  return (
    <svg viewBox="0 0 24 24" fill="currentColor" {...props}>
      <path d="..." />
    </svg>
  );
}
```

- Use `currentColor` for fills so icons inherit text color
- Spread `{...props}` onto `<svg>` for sizing
- Size via `style={{ width, height }}` from the call site
- Brand/social marks go in `elements/icons/social/`

## Modal System

Modals use a provider pattern split between `runtime/` and `patterns/`:

- `runtime/modals/` — Provider and renderer (infrastructure)
- `patterns/modals/` — Concrete modal components
- Modals are mutually exclusive — opening a new one closes the previous
- Optional `getUnmountDelayMS()` via `useImperativeHandle` for exit animations
