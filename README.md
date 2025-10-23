# Inventory Manager

A lightweight inventory management web app built with Next.js, TypeScript and Prisma. It provides basic product CRUD, pagination, charts for inventory, and a seeded demo dataset.

Repository: https://github.com/adil162006/Inventory-management

## Features

- Next.js 15 (App Router) + TypeScript
- Prisma (PostgreSQL) with a Product model
- Simple authentication placeholder (stack auth userId stored on products)
- Seed script that creates 25 demo products
- Dashboard with products chart and inventory listing

## Quick links

- App source: `myapp/app`
- Server code / API actions: `myapp/lib` and `myapp/app/*`
- Prisma schema & seed: `myapp/prisma`

## Requirements

- Node.js 18+ (use the version that works with Next 15)
- npm (or yarn / pnpm)
- PostgreSQL database (local or hosted)

## Clone

Open a terminal and run:

```powershell
git clone https://github.com/adil162006/Inventory-management.git
cd "Inventory-management/myapp"
```

## Environment

Create a `.env` file in `myapp/` (next to `package.json`). Required variables:

- `DATABASE_URL` — a PostgreSQL connection string. Example:

```text
DATABASE_URL="postgresql://USER:PASSWORD@localhost:5432/inventory_db"
```

Optional: set any other environment variables required by your deployment or auth provider.

## Install

From the `myapp` folder run:

```powershell
npm install
```

## Database setup (Prisma)

Run migrations (if you need to create the database tables) and generate the Prisma Client:

```powershell
npx prisma migrate deploy    # apply migrations (use migrate dev for local development if preferred)
npx prisma generate
```

If you don't have existing migrations or want to create a development migration, run:

```powershell
npx prisma migrate dev --name init
```

## Seed demo data

This project includes a seed script configured in `package.json`:

```json
"prisma": {
	"seed": "ts-node --esm prisma/seed.ts"
}
```

Seed the database (from `myapp`):

```powershell
npx prisma db seed
```

The seed script creates 25 demo products for a demo user ID. You can inspect or change `myapp/prisma/seed.ts` to alter the data.

## Development

Run the Next.js dev server:

```powershell
npm run dev
```

Open http://localhost:3000 to view the app.

Available npm scripts (from `myapp/package.json`):

- `dev` — run Next.js in development (uses Turbopack)
- `build` — build for production
- `start` — run production server
- `lint` — run ESLint

## Build & Production

Build the app:

```powershell
npm run build
```

Start the production server (after build):

```powershell
npm run start
```

For Vercel deployment, push the `myapp` folder as the project root or configure the repo to use `myapp` as the build output directory.

## Prisma schema (summary)

The project uses a PostgreSQL datasource and defines a `Product` model with fields:

- `id` (cuid)
- `userId` (string) — Stack Auth user id reference
- `name`, `sku`, `price` (Decimal), `quantity`, `lowStockAt`
- `createdAt`, `updatedAt`

See `myapp/prisma/schema.prisma` for the full schema.

## Notes & Next steps

- If you plan to run this in production, secure your `DATABASE_URL` and any other secrets.
- Consider swapping the demo user id in the seed script for real auth integration.
- Add CI (lint/test/build) and database backups for production readiness.

## Project structure (top-level)

- `myapp/` — Next.js application root
	- `app/` — Next.js App Router pages and components
	- `lib/` — helper libs (Prisma client, auth helpers, actions)
	- `prisma/` — Prisma schema, seed script and migrations
	- `public/` — static assets

## License

Include your preferred license file if you want to open-source this repo.

---

If you want, I can also:

- Add a CONTRIBUTING.md with local dev workflow
- Add GitHub Actions for lint/build
- Prepare a docker-compose example for Postgres + app

Tell me which of those you'd like next.

Try it (quick commands)

```powershell
git clone https://github.com/adil162006/Inventory-management.git
cd "Inventory-management/myapp"
# create .env and set DATABASE_URL, for example:
# DATABASE_URL="postgresql://USER:PASSWORD@localhost:5432/inventory_db"
npm install
# apply migrations (or use `migrate dev` for local dev)
npx prisma migrate deploy
npx prisma generate
# optionally, create a local migration instead:
npx prisma migrate dev --name init
```
