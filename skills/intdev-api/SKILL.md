---
name: intdev-api
description: Integrate with api.internet.dev — INTDEV's white-label API for authentication, payments, data storage, organizations, marketplace, and more. Use when building applications that need user auth, Stripe payments, file uploads, or any backend services provided by the INTDEV API.
license: MIT
metadata:
  author: internet-development
  version: "1.0"
---

# INTDEV API

## Overview

The INTDEV API at [api.internet.dev](https://api.internet.dev) is a white-label ready API for internal services and client builds. It provides authentication, payments (Stripe), file storage (S3/GCS), data management, organizations, marketplace, and more — all as Next.js API routes backed by PostgreSQL.

- **Base URL**: `https://api.internet.dev`
- **Repository**: [internet-development/apis](https://github.com/internet-development/apis)
- **Stack**: Next.js, TypeScript, PostgreSQL (via Knex), Stripe, AWS S3, Google Cloud Storage

## Authentication

The API uses API key + optional session-based authentication.

### Sign Up / Sign In

```
POST /api/users/authenticate
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "..."
}
```

Returns a user object with an API key. Store the API key for subsequent requests.

### Authenticated Requests

Pass the API key via the `Authorization` header:

```
Authorization: Bearer <api-key>
```

### Auth Providers

| Endpoint | Provider |
|----------|----------|
| `POST /api/users/authenticate` | Email + password |
| `POST /api/users/authenticate-apple-client` | Apple Sign-In |
| `GET /api/users/viewer` | Get current user from API key |
| `POST /api/users/verify` | Email verification |
| `POST /api/users/reset-password` | Password reset |

### Quick Start Template

For a pre-wired auth + payments setup, use [nextjs-intdev-services-auth-payments](https://github.com/internet-development/nextjs-intdev-services-auth-payments).

## Core API Domains

### Users

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/users` | GET | List users |
| `/api/users/viewer` | GET | Get authenticated user |
| `/api/users/get-by-id` | GET | Get user by ID |
| `/api/users/update` | POST | Update user profile |
| `/api/users/delete` | POST | Delete user |
| `/api/users/regenerate-key` | POST | Generate new API key |

### Organizations

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/organizations` | GET | List organizations |
| `/api/organizations/create` | POST | Create organization |
| `/api/organizations/get-by-id` | GET | Get org by ID |
| `/api/organizations/users` | GET | List org members |
| `/api/organizations/users/add` | POST | Add member |
| `/api/organizations/users/remove` | POST | Remove member |
| `/api/organizations/users/promote` | POST | Promote to admin |
| `/api/organizations/users/demote` | POST | Demote from admin |

### Data (Generic Storage)

A flexible key-value style data store for arbitrary content.

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/data` | GET | List data entries |
| `/api/data/delete` | POST | Delete entry |
| `/api/data/things` | GET | List "things" (typed data objects) |
| `/api/data/things/create` | POST | Create a thing |
| `/api/data/things/update` | POST | Update a thing |
| `/api/data/things/delete` | POST | Delete a thing |
| `/api/data/things/list/search` | GET | Search things |

### File Storage

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/data/generate-presigned-url` | POST | Get AWS S3 presigned upload URL |
| `/api/data/generate-presigned-url-gcs` | POST | Get GCS presigned upload URL |

Upload flow:
1. Request a presigned URL from the API
2. Upload the file directly to S3/GCS using the presigned URL
3. Store the resulting URL in your data model

### Posts & Threads

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/posts` | GET | List posts |
| `/api/posts/create` | POST | Create post |
| `/api/posts/update` | POST | Update post |
| `/api/posts/delete` | POST | Delete post |
| `/api/posts/all-threads` | GET | List all threads |
| `/api/posts/all-thread-replies` | GET | Get thread replies |
| `/api/posts/public/[slug]` | GET | Get public post by slug |

### Documents

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/documents` | GET | List documents |
| `/api/documents/create` | POST | Create document |
| `/api/documents/update` | POST | Update document |
| `/api/documents/delete` | POST | Delete document |
| `/api/documents/[id]` | GET | Get document by ID |

### Payments (Stripe)

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/users/subscriptions` | GET | List user subscriptions |
| `/api/users/subscriptions/check` | GET | Check subscription status |
| `/api/users/subscriptions/unsubscribe` | POST | Cancel subscription |
| `/api/users/viewer/generate-add-payment-method-url` | POST | Get Stripe payment setup URL |
| `/api/users/viewer/get-current-payment-method` | GET | Get current payment method |
| `/api/users/viewer/pay-provider-amount-cents` | POST | Make a payment |
| `/api/webhooks/stripe` | POST | Stripe webhook handler |

### Credits System

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/credits` | GET | Credits overview |
| `/api/credits/get-balance-by-user-id` | GET | Get user credit balance |
| `/api/credits/deduct` | POST | Deduct credits |
| `/api/credits/send` | POST | Send credits to another user |
| `/api/credits/create-account-by-user-id` | POST | Create credits account |

### Marketplace

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/marketplace/cart` | GET | Get cart contents |
| `/api/marketplace/cart/add` | POST | Add item to cart |
| `/api/marketplace/cart/remove` | POST | Remove item from cart |
| `/api/marketplace/checkout` | POST | Process checkout |
| `/api/marketplace/orders` | GET | List orders |
| `/api/marketplace/discounts` | GET | List discount codes |

### Events

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/events` | GET | List events |
| `/api/events/create` | POST | Create event |
| `/api/events/update` | POST | Update event |
| `/api/events/delete` | POST | Delete event |

### Monitoring

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/monitors` | GET | List monitors |
| `/api/monitors/create` | POST | Create monitor |
| `/api/monitors/validation` | GET | Run monitor validation |
| `/api/status` | GET | API health check |

## Local Development

```bash
git clone https://github.com/internet-development/apis.git
cd apis
npm install
npm run dev
```

Runs on `http://localhost:10001` (note: port 10001, not 10000).

### Environment Variables

```env
API_DATABASE_NAME=xxxx
API_DATABASE_USERNAME=xxxx
API_DATABASE_HOST=xxxx
API_DATABASE_PORT=5432
API_DATABASE_PASSWORD=xxxx
```

### Running Scripts

```bash
npm run script example       # Run a script
npm run worker example       # Run a background worker
```

## Integration Pattern

The standard pattern for integrating with the INTDEV API from a Next.js frontend:

```tsx
const API_URL = 'https://api.internet.dev';

async function fetchWithAuth(endpoint: string, options: RequestInit = {}) {
  const apiKey = getCookie('api_key'); // or from state/context
  const response = await fetch(`${API_URL}${endpoint}`, {
    ...options,
    headers: {
      'Content-Type': 'application/json',
      'Authorization': `Bearer ${apiKey}`,
      ...options.headers,
    },
  });
  return response.json();
}

// Example: Get current user
const viewer = await fetchWithAuth('/api/users/viewer');

// Example: Create a post
const post = await fetchWithAuth('/api/posts/create', {
  method: 'POST',
  body: JSON.stringify({ title: 'Hello', body: 'World' }),
});
```
