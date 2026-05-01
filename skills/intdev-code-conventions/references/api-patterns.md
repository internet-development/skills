# API Patterns

## Route Wrapper

All API routes use `Server.api()`:

```typescript
import * as Server from '@common/server';

export default Server.api(async function apiUsersViewer(req, res) {
  const user = await getUser(req);
  if (!user) {
    return res.status(401).json({ error: true, message: 'Not authenticated.' });
  }
  return res.status(200).json({ user });
});
```

`Server.api()` handles: CORS, rate limiting (in-memory fixed-window counter), exception reporting, `_usage` metadata injection.

Routes do NOT enforce HTTP methods — the wrapper handles method filtering via `common/api-route-config.ts`.

## Response Shapes

Two canonical shapes. Follow them exactly.

**Success:**
```json
{ "user": { ... }, "existing": true }
{ "data": [ ... ], "success": true }
```

**Error:**
```json
{ "error": true, "message": "Description of what went wrong." }
```

Every response automatically includes a `_usage` field with token cost and rate limit data.

## Rate Limiting

Defined in `common/api-route-config.ts`:

```typescript
{
  route: '/api/users/viewer',
  method: 'POST',
  cost: 1,
  category: 'read',
}
```

Categories: `read`, `write`, `financial`, `auth`, `beacon`, `unlimited`.

Tier-based multipliers:
| Tier | Multiplier |
|------|-----------|
| UNVERIFIED | 1x |
| VERIFIED | 6x |
| PAYING | 12x |
| ADMIN | unlimited |

## Input Validation

No schema validation library (no Zod, no Joi) in frontend/API repos. Use `Utilities.isEmpty()`:

```typescript
if (Utilities.isEmpty(req.body.email)) {
  return res.status(400).json({ error: true, message: 'Email is required.' });
}
```

Agent/tool repos (`daedalus`, `ts-general-agent`) use Zod for structured agent output, but not for HTTP input validation.

## Auth

Auth via `X-API-KEY` header:

```typescript
const response = await fetch(route, {
  method: 'POST',
  headers: {
    'X-API-KEY': key,
    'Content-Type': 'application/json',
  },
  body: JSON.stringify(body),
});
```

Session management through the API's `/api/users/authenticate` endpoint. No client-side JWT libraries.

## Sensitive Field Sanitization

Before returning user objects, always strip sensitive fields:

```typescript
delete user.hash;
delete user.wallet_signature;
delete user.created_at;
delete user.deleted_at;
delete user.updated_at;
delete user.key;
```

## Adapter Return Type (Agent Repos)

In `ts-general-agent` and `daedalus`, all adapter functions return `ApiResult<T>`:

```typescript
type ApiResult<T> =
  | { success: true; data: T }
  | { success: false; error: string };
```

This pattern is for agent/tool repos only. The API (`apis` repo) uses the response shapes above.
