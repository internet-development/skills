---
name: intdev-deployment
description: Deploy and maintain INTDEV websites and applications using Render, Vercel, and AWS. Covers deployment configuration, environment setup, PostgreSQL databases, S3 asset hosting, and maintenance patterns for Next.js projects built with nextjs-sass-starter.
license: MIT
metadata:
  author: internet-development
  version: "1.0"
---

# INTDEV Deployment

## Overview

INTDEV deploys and maintains websites using a combination of Render (primary hosting), Vercel (static/serverless), and AWS (S3 for assets, EC2 for specialized workloads). All INTDEV projects are Next.js applications that follow the same deployment patterns.

**Keywords**: deployment, hosting, Render, Vercel, AWS, S3, PostgreSQL, environment variables, CI/CD, maintenance

## Hosting Providers

### Render (Primary)

Most INTDEV production sites run on [Render.com](https://render.com). Key conventions:

- **Port**: All INTDEV apps run on port `10000` (Render's default expectation)
- **Build command**: `npm run build`
- **Start command**: `npm run start`
- **Node.js version**: >= 18

The `package.json` scripts are already configured for Render:

```json
{
  "scripts": {
    "dev": "next -p 10000",
    "build": "next build",
    "start": "PORT=10000 next start"
  }
}
```

#### Render Configuration

When setting up a new Render Web Service:

1. Connect the GitHub repository
2. Set **Build Command**: `npm install && npm run build`
3. Set **Start Command**: `npm run start`
4. Set **Node Version**: 18+ (via environment variable `NODE_VERSION=20`)
5. Add environment variables as needed

### Vercel

Some INTDEV sites use [Vercel](https://vercel.com) for hosting, especially the component libraries:

- Sacred Computer ([sacred.computer](https://sacred.computer)) — hosted on Vercel
- Server Mono site — hosted on Vercel

Vercel requires no special configuration for Next.js projects. Just connect the repo and deploy.

### AWS

INTDEV uses AWS for:

- **S3**: Static asset hosting (images, fonts, files)
  - Primary bucket: `intdev-global.s3.us-west-2.amazonaws.com`
  - Public assets served from: `intdev-global.s3.us-west-2.amazonaws.com/public/internet-dev/`
- **Presigned URLs**: File uploads go through S3 presigned URLs via the API
- **EC2**: Specialized workloads when needed

## Database

INTDEV uses **PostgreSQL** for all persistent data, accessed via [Knex.js](https://knexjs.org/) query builder.

### Environment Variables

```env
API_DATABASE_NAME=your_db_name
API_DATABASE_USERNAME=your_db_user
API_DATABASE_HOST=your_db_host
API_DATABASE_PORT=5432
API_DATABASE_PASSWORD=your_db_password
```

### Database Providers

- **Render PostgreSQL** — For Render-hosted apps
- **AWS RDS** — For production workloads
- **Local PostgreSQL** — For development (default port 5432)

## CDN & Assets

### Static Assets

INTDEV serves static assets from S3:

```
https://intdev-global.s3.us-west-2.amazonaws.com/public/internet-dev/{asset-id}.{ext}
```

### Fonts

Server Mono is served via jsDelivr CDN:

```
https://cdn.jsdelivr.net/gh/internet-development/www-server-mono@latest/public/fonts/
```

### CORS

For S3 buckets that serve assets to web apps, the CORS configuration:

```json
[
  {
    "AllowedHeaders": ["*"],
    "AllowedMethods": ["GET", "PUT", "POST"],
    "AllowedOrigins": ["*"],
    "ExposeHeaders": []
  }
]
```

## Environment Variables

Common environment variables across INTDEV projects:

| Variable | Used By | Description |
|----------|---------|-------------|
| `API_DATABASE_*` | apis | PostgreSQL connection |
| `STRIPE_SECRET_KEY` | apis | Stripe payments |
| `STRIPE_WEBHOOK_SECRET` | apis | Stripe webhook verification |
| `AWS_ACCESS_KEY_ID` | apis | AWS S3 access |
| `AWS_SECRET_ACCESS_KEY` | apis | AWS S3 secret |
| `GOOGLE_CLOUD_*` | apis | GCS credentials |
| `NODE_VERSION` | Render | Node.js version |
| `PORT` | All | Server port (default: 10000) |

**Important**: Never commit `.env` files. The `.gitignore` in INTDEV projects excludes `.env` by default.

## Port Conventions

| Port | Service |
|------|---------|
| `10000` | Frontend web applications (nextjs-sass-starter, www-sacred, etc.) |
| `10001` | API server (apis) |
| `5432` | PostgreSQL (default) |

## Deployment Checklist

When deploying a new INTDEV project:

1. **Repository setup** — Ensure `.gitignore` includes `.env`, `.next/`, `node_modules/`
2. **Port configuration** — Verify `dev` and `start` scripts use port 10000
3. **Environment variables** — Set all required env vars in the hosting provider
4. **Database** — Provision PostgreSQL if the project needs it, run any SQL migrations from `sql/`
5. **DNS** — Configure custom domain and SSL
6. **Health check** — Verify `/api/status` returns 200 (if using the INTDEV API)
7. **Monitoring** — Set up uptime monitoring via `/api/monitors`

## Maintenance

- INTDEV sites are designed for low-maintenance operation
- Node.js and dependency updates are managed via `npm update` and periodic major version bumps
- Database backups should be configured through the hosting provider
- S3 assets are durable by default (99.999999999% durability)
