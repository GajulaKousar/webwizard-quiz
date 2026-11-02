# Web Wizard — Render + Neon deployment

This version uses Express + Neon PostgreSQL (the previous Turso/Vercel adapter has been removed).

## Render settings
- Root Directory: `web-wizard` (only if the repository contains the outer folder; otherwise leave blank)
- Runtime: Node
- Build Command: `npm install`
- Start Command: `npm start`
- Plan: Free
- Health Check Path: `/health`

## Required environment variables
- `DATABASE_URL`: Neon PostgreSQL connection string (copy the pooled connection string from Neon; it begins with `postgresql://` and normally contains `-pooler` in the hostname).
- `SESSION_SECRET`: a long random secret, at least 32 characters.
- `ADMIN_USER`: admin username (defaults to `kavya` if omitted).
- `ADMIN_PASS`: choose a strong admin password. Required for a secure setup; set it before the first app request.
- `TEAM_COUNT`: number of participant teams to create (defaults to 60; creates `01` through `60`).
- `PASS_PREFIX`: optional participant password prefix (defaults to `wizard`; team `01` uses `wizard01`).
- `TEAMS`: optional comma-separated exact team list; if set, it takes precedence over `TEAM_COUNT`.

The database tables, administrator, and participant accounts are initialized automatically on the first API request. Existing accounts are not overwritten. Changing the admin password environment variable later does not change an already-created admin account; update it in the database or recreate the database if this is a fresh test deployment.

## Important free-tier notes
Render free web services sleep after 15 minutes without traffic and may take around a minute to wake. Neon free plan limits may change; check your Neon dashboard for current quotas. This is suitable for testing/event trials, not guaranteed always-on production hosting.

## Local run
1. Create a Neon database and put its connection string in `DATABASE_URL`.
2. Set `SESSION_SECRET` (32+ characters) and `ADMIN_PASS` in your environment.
3. Run `npm install`, then `npm start`.
