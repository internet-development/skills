# File Organization

## Naming Conventions

| Type | Convention | Examples |
|------|-----------|----------|
| **Component files** | PascalCase | `Button.tsx`, `ActionBar.tsx`, `DropdownMenu.tsx` |
| **Component styles** | PascalCase, matching component | `Button.module.css`, `ActionBar.module.css` |
| **Utility files** | camelCase | `utilities.ts`, `constants.ts`, `queries.ts` |
| **Directories** | lowercase, singular when a category | `components/`, `common/`, `modules/`, `runtime/` |
| **Pages** | lowercase or kebab-case | `pages/examples/accordion.tsx` |
| **CSS classes** | camelCase (via CSS Modules) | `.root`, `.actionButton`, `.leftPanel` |
| **CSS variables** | kebab-case with prefix | `--theme-background`, `--color-gray-60` |
| **TypeScript types** | PascalCase | `ApiResult<T>`, `UserResponse` |
| **Functions** | camelCase | `getData()`, `classNames()`, `isEmpty()` |
| **Constants** | UPPER_SNAKE_CASE or camelCase | `API_URL`, `apiVersion` |
| **Vendored modules** | lowercase kebab-case directory | `modules/object-assign/index.ts` |
| **Icon components** | PascalCase with `Icon` prefix | `IconArrow.tsx`, `IconCheck.tsx` |

## Colocated Files

Every component is a pair: one `.tsx` file and one `.module.css` file, same name, same directory.

```
components/
  Button.tsx
  Button.module.css
  Card.tsx
  Card.module.css
  Dialog.tsx
  Dialog.module.css
```

No `index.ts` barrel files. No grouping components into subdirectories unless they form a distinct tier (see [component-tiers.md](component-tiers.md)).

## Directory Structure

Standard INTDEV project layout:

```
project/
├── app/                  # App Router (metadata only — layout, manifest, robots, sitemap)
├── pages/                # Pages Router (all actual routes)
│   ├── _app.tsx
│   ├── _document.tsx
│   └── examples/
├── components/           # React components (or tiered: elements/, components/, patterns/)
├── common/               # Shared utilities, constants, queries
│   ├── utilities.ts
│   ├── constants.ts
│   └── queries.ts
├── modules/              # Vendored zero-dependency code
├── public/               # Static assets
├── global.css            # Global styles, CSS reset, font-face, theme definitions
├── .prettierrc           # Prettier config
├── tsconfig.json
└── package.json
```

## Path Aliases

All INTDEV projects define path aliases in `tsconfig.json` to avoid relative imports across top-level directories:

```json
{
  "compilerOptions": {
    "paths": {
      "@components/*": ["components/*"],
      "@common/*": ["common/*"],
      "@modules/*": ["modules/*"],
      "@elements/*": ["elements/*"],
      "@patterns/*": ["patterns/*"],
      "@data/*": ["data/*"],
      "@runtime/*": ["runtime/*"]
    }
  }
}
```

**Rule**: Never use `../../` to cross top-level directory boundaries. Use path aliases instead.

```typescript
// GOOD
import Button from '@components/Button';
import * as Utilities from '@common/utilities';

// BAD
import Button from '../../components/Button';
import * as Utilities from '../../../common/utilities';
```

Relative imports are fine within the same directory (e.g., `./Button.module.css`).

## Import Ordering

Imports follow a strict order with blank lines between groups:

```typescript
// 1. Styles (CSS Module for this component)
import styles from './Component.module.css';

// 2. React (always namespace import)
import * as React from 'react';

// 3. Common utilities and constants (namespace imports)
import * as Constants from '@common/constants';
import * as Utilities from '@common/utilities';

// 4. Data/queries
import * as Query from '@data/query';

// 5. Components by tier (elements first, then components, then patterns)
import Button from '@elements/Button';
import Card from '@components/Card';
import PageLayout from '@patterns/PageLayout';

// 6. Relative imports (same directory)
import { someHelper } from './helpers';
```

### Namespace Import Rule

React and utility modules always use namespace imports:

```typescript
// GOOD
import * as React from 'react';
import * as Utilities from '@common/utilities';

// BAD — never destructure these
import React, { useState, useEffect } from 'react';
import { classNames } from '@common/utilities';
```

Hooks are called as `React.useState()`, `React.useCallback()`, etc.

Component imports use default imports:

```typescript
import Button from '@components/Button';
import Navigation from '@components/Navigation';
```

## Vendored Modules

The `modules/` directory contains self-contained, zero-dependency code that would otherwise be an npm package:

```
modules/
  aes/index.ts         # AES encryption
  cookies/index.ts     # Cookie parsing
  cors/index.ts        # CORS headers
  hotkeys/index.ts     # Keyboard shortcuts (vendored react-hotkeys-hook)
  vary/index.ts        # Vary header
```

**Rule**: If a package does one thing and is small, vendor it in `modules/` instead of adding it to `package.json`. This keeps the dependency tree minimal and the code auditable.
