# Prisma Practice

A small TypeScript project for learning and practicing [Prisma ORM](https://www.prisma.io/) with PostgreSQL.

## Stack

- **Node.js** with ES modules
- **TypeScript**
- **Prisma 7** — schema, migrations, and client
- **PostgreSQL** — via `pg` and `@prisma/adapter-pg`
- **tsx** — run TypeScript without a separate build step

## Prerequisites

- [Node.js](https://nodejs.org/) (v18 or later recommended)
- [PostgreSQL](https://www.postgresql.org/) running locally or accessible remotely

## Getting started

### 1. Install dependencies

```bash
npm install
```

### 2. Initialize Prisma

If you have not set up Prisma yet:

```bash
npx prisma init
```

This creates `prisma/schema.prisma` and `prisma.config.ts`.

### 3. Configure the database

Create a `.env` file in the project root:

```env
DATABASE_URL="postgresql://USER:PASSWORD@localhost:5432/prisma_practice?schema=public"
```

Replace `USER`, `PASSWORD`, and the database name with your local PostgreSQL credentials.

### 4. Define your schema

Edit `prisma/schema.prisma` with your models, then create and apply your first migration:

```bash
npx prisma migrate dev --name init
```

### 5. Generate the client

```bash
npx prisma generate
```

The client is regenerated automatically by `migrate dev`, but run this manually after `db pull` or when the client is out of date.

## Project structure

```
prisma-practice/
├── prisma/
│   └── schema.prisma      # Database models (after init)
├── prisma.config.ts       # Prisma configuration (after init)
├── doc/
│   └── prisma-commands.md # Prisma CLI command reference
├── .env                   # Database URL (not committed)
├── package.json
└── tsconfig.json
```

## Prisma commands

See **[doc/prisma-commands.md](./doc/prisma-commands.md)** for a full list of commands, including:

- `prisma migrate dev` — create and apply migrations
- `prisma db push` — push schema changes without migrations
- `prisma studio` — browse and edit data in the browser
- `prisma generate` — regenerate the Prisma Client

## Scripts

Add npm scripts to `package.json` as you build out the project. Common examples:

```json
{
  "scripts": {
    "db:generate": "prisma generate",
    "db:migrate": "prisma migrate dev",
    "db:push": "prisma db push",
    "db:studio": "prisma studio"
  }
}
```

## Resources

- [Prisma Docs](https://www.prisma.io/docs)
- [Prisma PostgreSQL guide](https://www.prisma.io/docs/orm/overview/databases/postgresql)
- [Prisma Migrate](https://www.prisma.io/docs/orm/prisma-migrate)
