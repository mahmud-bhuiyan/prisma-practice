# Prisma Commands Reference

Quick reference for the Prisma CLI commands used in this project.

Run commands with `npx prisma <command>` from the project root.

---

## Setup

```bash
# Initialize Prisma (creates prisma/schema.prisma and prisma.config.ts)
npx prisma init

# Check installed Prisma version
npx prisma version
```

---

## Schema

```bash
# Validate schema.prisma
npx prisma validate

# Format schema.prisma
npx prisma format
```

---

## Client

```bash
# Generate Prisma Client after schema changes
npx prisma generate
```

Run `generate` after every schema change, or after `migrate dev` / `db pull`.

---

## Database — prototyping

Use these when experimenting and you do not need migration history yet.

```bash
# Push schema changes directly to the database (no migration files)
npx prisma db push

# Pull an existing database schema into schema.prisma (introspection)
npx prisma db pull

# Run seed script (defined in package.json "prisma.seed")
npx prisma db seed

# Execute a SQL file against the database
npx prisma db execute --file ./script.sql
```

---

## Migrations — development

Use these once you want tracked, versioned schema changes.

```bash
# Create a migration from schema changes and apply it
npx prisma migrate dev

# Create a named migration
npx prisma migrate dev --name add_user_table

# Reset database: drop, re-apply all migrations, run seed
npx prisma migrate reset
```

---

## Migrations — production / staging

```bash
# Apply pending migrations (CI/CD, deploy)
npx prisma migrate deploy

# Check which migrations have been applied
npx prisma migrate status

# Mark a migration as applied or rolled back (troubleshooting)
npx prisma migrate resolve --applied "20240101000000_init"
npx prisma migrate resolve --rolled-back "20240101000000_init"
```

---

## Compare schemas

```bash
# Diff two schema sources and output SQL
npx prisma migrate diff \
  --from-schema-datamodel prisma/schema.prisma \
  --to-url "$DATABASE_URL" \
  --script
```

---

## Prisma Studio

```bash
# Open a browser UI to view and edit data
npx prisma studio
```

---

## Useful flags

| Flag | Description |
|------|-------------|
| `--schema=./prisma/schema.prisma` | Use a custom schema path |
| `--config=./prisma.config.ts` | Use a custom Prisma config path |
| `--force` | Skip confirmation prompts (e.g. `db push`, `migrate reset`) |

---

## Typical workflow

### First-time setup

1. `npx prisma init`
2. Set `DATABASE_URL` in `.env`
3. Edit `prisma/schema.prisma`
4. `npx prisma migrate dev --name init`
5. `npx prisma generate`

### Day-to-day development

1. Edit `prisma/schema.prisma`
2. `npx prisma migrate dev --name describe_change`
3. Use the generated client in your TypeScript code

### Quick prototype (no migrations)

1. Edit `prisma/schema.prisma`
2. `npx prisma db push`
3. `npx prisma generate`

---

## Environment

This project uses **PostgreSQL** with the `@prisma/adapter-pg` driver adapter (Prisma 7).

Example `.env`:

```env
DATABASE_URL="postgresql://USER:PASSWORD@localhost:5432/prisma_practice?schema=public"
```

Never commit `.env` — it is listed in `.gitignore`.
