# Tooling

## Prettier

The same `.prettierrc` across every INTDEV repo:

```json
{
  "bracketSpacing": true,
  "printWidth": 9999,
  "semi": true,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "es5",
  "overrides": [
    {
      "files": ["*.scss", "*.css"],
      "options": {
        "parser": "scss"
      }
    }
  ]
}
```

**`printWidth: 9999` is intentional.** Long lines are expected. No line wrapping. This is a core convention, not an accident.

The CSS override uses `scss` parser even for `.css` files — this ensures consistent formatting across legacy SCSS and modern CSS projects.

## No Linter

INTDEV repos do not use ESLint, Biome, or any linter. The build (`next build`) is the only code quality gate — it typechecks via TypeScript.

Don't add ESLint configs, lint scripts, or lint-staged. Don't suggest adding them.

## No Test Runner in Frontend

Frontend repos (nextjs-sass-starter, nextjs-css-agent-components) have no test harness. Don't write tests, don't add test frameworks.

```
# From AGENTS.md:
# Don't write new tests — there is no harness. Don't add documentation files unless asked.
```

**Exceptions:**
- `www-sacred` has vitest for the CLI framework (Simulacrum) parity tests
- `apis` has vitest for API route config and utility tests (`.spec.ts` colocated with source)
- `daedalus` and `ts-general-agent` have test suites

Follow whatever the existing project does.

## Build

Frontend projects:
```json
{
  "scripts": {
    "dev": "next dev -p 10000",
    "build": "next build",
    "start": "next start -p 10000",
    "prettier": "prettier --write ."
  }
}
```

API project:
```json
{
  "scripts": {
    "dev": "next -p 10001",
    "build": "next build",
    "start": "next start -p 10001"
  }
}
```

**Port convention**: `10000` for frontend, `10001` for API, `5432` for PostgreSQL.

## Vendored Modules

The `modules/` directory holds vendored, zero-dependency code:

```
modules/
  aes/index.ts
  cookies/index.ts
  cors/index.ts
  hotkeys/index.ts
  vary/index.ts
  object-assign/index.ts
```

**When to vendor**: If a package does one focused thing, has few lines of code, and would add transitive dependencies to `package.json`, vendor it instead.

**When NOT to vendor**: Large frameworks (React, Next.js), complex packages with ongoing security patches (crypto libraries), packages with many files.

## Dependencies Philosophy

Minimal. The `www-sacred` `package.json` has 3 production dependencies: `next`, `react`, `react-dom`. That's it.

- No Tailwind, no styled-components, no Emotion
- No lodash, no date-fns, no moment
- No clsx, no classnames
- No React Query, no SWR, no TanStack
- No ESLint, no Biome
- No Storybook

Use the built-in utilities from `common/utilities.ts` for anything these packages would provide.

## AGENTS.md Convention

Every major INTDEV repo has an `AGENTS.md` at root — a machine-oriented operating manual for AI coding agents. These are not READMEs. They contain:
- Exact file maps and architectural rules
- Verbatim code patterns to replicate
- Convention checklists
- What NOT to do

Some repos also expose these at stable URLs (`/llm/AGENTS.md`, `/SKILL.md`) following the [llmstxt.org](https://llmstxt.org/) convention.

## next.config.ts

```javascript
const nextConfig = {
  devIndicators: false,
  typescript: { ignoreBuildErrors: false },
};
```

`devIndicators: false` removes Next.js dev overlay. `ignoreBuildErrors: false` ensures TypeScript errors fail the build.

## Pages Router Primary

INTDEV frontend projects use Pages Router for all actual routes:
- `pages/_app.tsx` — App wrapper
- `pages/_document.tsx` — HTML document (sets `body` class to `theme-light`)
- `pages/examples/**` — Feature pages

App Router (`app/`) is used **only for metadata**: layout, manifest, robots, sitemap. Do not migrate routes to App Router unless explicitly asked.

**Exception**: `www-sacred` uses full App Router.
