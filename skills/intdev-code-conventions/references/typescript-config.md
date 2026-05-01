# TypeScript Configuration

## Two Profiles

INTDEV uses different TypeScript strictness depending on the project type.

### Frontend Projects (Relaxed)

Used in: `www-sacred`, `nextjs-sass-starter`, `nextjs-css-agent-components`, `apis`

```json
{
  "compilerOptions": {
    "strict": false,
    "strictNullChecks": true,
    "target": "es5",
    "lib": ["dom", "dom.iterable", "esnext"],
    "module": "esnext",
    "moduleResolution": "bundler",
    "jsx": "preserve",
    "allowJs": true,
    "skipLibCheck": true,
    "esModuleInterop": true,
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "incremental": true,
    "paths": {
      "@components/*": ["components/*"],
      "@common/*": ["common/*"],
      "@modules/*": ["modules/*"]
    }
  }
}
```

Key points:
- `strict: false` but `strictNullChecks: true` — catch null errors without verbose type annotations everywhere
- No explicit Props interfaces on components
- `target: "es5"` or `"es6"` for broad browser support

### Agent/Tool Projects (Strict)

Used in: `ts-general-agent`, `daedalus`

```json
{
  "compilerOptions": {
    "strict": true,
    "strictNullChecks": true,
    "target": "ES2022",
    "module": "NodeNext",
    "moduleResolution": "NodeNext",
    "outDir": "./dist",
    "rootDir": "./src",
    "declaration": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true
  }
}
```

Key points:
- `strict: true` with full type safety
- `module: "NodeNext"` with file extensions in imports: `./module.js`
- `type: "module"` in `package.json`
- Explicit interfaces and type annotations

## Which Profile to Use

Follow whatever the existing project uses. If starting a new project:
- **Web app / website** → Relaxed profile
- **CLI tool / library / agent** → Strict profile

## next.config

Frontend projects use minimal config:

```javascript
const nextConfig = {
  devIndicators: false,
  typescript: { ignoreBuildErrors: false },
};
```

`ignoreBuildErrors: false` — TypeScript errors fail the build. This is the only code quality gate.
