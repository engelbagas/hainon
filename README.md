# HAINON GLOBAL PRO

Starter project for an Arabic RTL PPPoE subscription management platform.

## Included in this first scaffold

- Responsive Arabic dashboard UI with role preview for admin, premium supervisor, support, and subscriber.
- Sample dashboard statistics, payment requests, and subscriber table.
- Role preview order is subscriber, regular supervisor, premium supervisor, then main administrator.
- Sham Cash QR preview: administrator can change the image URL in the UI prototype; premium supervisor has view-only access.
- A local demo QR placeholder is included and is clearly marked as not real.
- Search/filter interaction, mobile sidebar, and illustrative add-subscriber modal.
- Initial Prisma/PostgreSQL data model for users, plans, subscriptions, payment requests, support messages, and audit logs.

## Important status

This is a **UI prototype and project scaffold**, not a production-ready service. Role switching is for preview only. The sample records are hard-coded. Authentication, server-enforced authorization, database persistence, Sham Cash verification, and MikroTik integration are not implemented yet. The QR URL edit currently changes only client-side preview state; it does not persist and must not be treated as a security boundary. Do not use real customer details or network credentials in this prototype.

## Requirements

- Node.js 20.9+ for Next.js 15
- npm
- PostgreSQL when you are ready to initialize the database

## Run locally

```bash
npm install
npm run dev
```

Open http://localhost:3000

## Database setup (next stage)

1. Copy `.env.example` to `.env`.
2. Set `DATABASE_URL` to your PostgreSQL connection string.
3. Install/generate Prisma client and run a migration:

```bash
npm install @prisma/client
npx prisma generate
npx prisma migrate dev --name init
```

The current Prisma schema uses Prisma ORM 6 syntax. Keep Prisma CLI and `@prisma/client` on matching major versions.

## Suggested implementation order

1. Add server-side authentication and role-based authorization, with default-deny permissions.
2. Add secure account creation and first-admin provisioning.
3. Add database-backed subscription and payment request routes.
4. Enforce Sham Cash image update permission on the server: only the main administrator can update it; premium supervisors can read it only.
5. Add audit logging and transaction-safe payment approval.
6. Verify Sham Cash transfers through an authorized process before activation.
7. Implement RouterOS API integration on the server only, with least-privilege credentials and network restrictions.
8. Add tests, backups, monitoring, and deployment configuration.

## Security notes

- Never store passwords as plain text; store only a strong password hash.
- Never expose PPPoE secrets, router credentials, database credentials, or payment provider keys in browser code.
- A submitted transaction reference is not proof of payment.
- Validate permissions on every server-side action, not only by hiding buttons in the UI.
