# Commenting Conventions

## The Rule

Comments explain **why**, never **what**. If the code needs a comment to explain what it does, rename the variable or function instead.

## Patterns

### `NOTE(@handle)`

Rationale comments. Explain a non-obvious decision, constraint, or workaround.

```typescript
// NOTE(jimmylee): We vendor this module because the npm package pulls in 14 transitive dependencies.
```

```typescript
// NOTE(caidanw): Safari doesn't support this API before 16.4, so we fall back to polling.
```

```css
/* NOTE(jimmylee): Using box-shadow instead of border to avoid layout shift on focus. */
```

### `TODO(@handle)`

Planned work. Always attributed to a person who owns the follow-up.

```typescript
// TODO(jimmylee)
// Obviously delete this once we implement a theme picker modal.
```

```typescript
// TODO(caidanw): Replace with proper rate limiting once we move to Redis.
```

## What NOT to Comment

**Don't describe what code does:**
```typescript
// BAD: Set the user's name
user.name = name;

// BAD: Loop through the items
for (const item of items) { ... }

// BAD: Check if the user is authenticated
if (!user) return;
```

**Don't add section dividers or decorative comments:**
```typescript
// BAD:
// ==========================================
// AUTHENTICATION
// ==========================================
```

**Don't add JSDoc for internal functions:**
```typescript
// BAD:
/**
 * @param {string} name - The name of the user
 * @param {number} age - The age of the user
 * @returns {User} The created user object
 */
function createUser(name, age) { ... }
```

**Don't reference tickets, PRs, or temporal context:**
```typescript
// BAD: Added for issue #234
// BAD: Fix from PR review
// BAD: New requirement from product meeting 2024-01-15
```

## Format Rules

- Use `//` for TypeScript/JavaScript, `/* */` for CSS, `#` for Python/Shell
- One space after the comment marker
- Attribution uses GitHub username: `@jimmylee`, `@caidanw`
- Multi-line TODOs: first line is `TODO(@handle)`, subsequent lines are indented explanation
- Keep comments on their own line above the code they reference, not inline at end of line
