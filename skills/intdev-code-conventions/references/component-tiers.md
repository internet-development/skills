# Component Tiers

## Three-Tier Architecture

INTDEV projects with enough components use a strict three-tier hierarchy. Components at each tier have explicit import rules.

```
elements/       # Tier 1 — Atoms
components/     # Tier 2 — Molecules
patterns/       # Tier 3 — Organisms
runtime/        # Non-visual infrastructure
```

### Tier 1: Elements (Atoms)

Self-contained primitives. Import **zero** in-repo components.

```
elements/
  Button.tsx
  Button.module.css
  Input.tsx
  Input.module.css
  Badge.tsx
  Badge.module.css
  Text.tsx
  Text.module.css
```

Elements may import from `@common/*` and `@modules/*` but never from `@components/*` or `@patterns/*`.

### Tier 2: Components (Molecules)

Compose **only Tier 1 elements**. Never import from `@patterns/*`.

```
components/
  Card.tsx           # may import Button, Badge, Text from @elements/
  Card.module.css
  ActionBar.tsx      # may import ActionButton from @elements/
  ActionBar.module.css
```

### Tier 3: Patterns (Organisms)

Compose **elements and components**. Full access to Tier 1 and Tier 2.

```
patterns/
  PageLayout.tsx      # may import from @elements/ and @components/
  PageLayout.module.css
  Navigation.tsx
  Navigation.module.css
```

### Runtime (Infrastructure)

Non-visual code: providers, context, detectors, modal managers. Not a component tier — provides infrastructure that patterns and pages consume.

```
runtime/
  modals/
    ModalProvider.tsx
    ModalRenderer.tsx
  providers/
    ThemeProvider.tsx
```

## Import Rules

| From \ To | elements | components | patterns | runtime | common |
|-----------|----------|------------|----------|---------|--------|
| **elements** | same-dir only | NO | NO | NO | YES |
| **components** | YES | same-dir only | NO | NO | YES |
| **patterns** | YES | YES | same-dir only | YES | YES |
| **pages** | YES | YES | YES | YES | YES |

**Cross-tier imports in the wrong direction are immediate red flags.** If a Tier 1 element needs to import a Tier 2 component, the architecture is wrong — either the element is actually a component, or the dependency needs to be inverted.

## When to Use Tiers

Not every INTDEV project uses the full three-tier system:

- **Small projects** — All components in a flat `components/` directory. No tiers needed.
- **Medium projects** — Components split into `elements/` and `components/` when the count exceeds ~20.
- **Large projects** (like SRCL, nextjs-css-agent-components) — Full three-tier with `elements/`, `components/`, `patterns/`, and `runtime/`.

Follow whatever structure the existing project uses. Don't introduce tiers to a flat project unless asked.

## Page Shell Pattern

Every page wraps in a standard shell:

```tsx
<Page title="Page Title" description="..." url="https://...">
  <Navigation />
  <SomeLayout>
    {/* page content */}
  </SomeLayout>
  <GlobalModalManager />
</Page>
```

`Page` handles metadata. `Navigation` is always present. Layout components (`AppLayout`, `ThinAppLayout`, `SidebarLayout`) wrap content. `GlobalModalManager` handles modal rendering.
