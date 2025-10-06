# LibreTV (Minimal, Ready-to-Deploy)

This is a **fully deployable** minimal version of LibreTV on Cloudflare Workers.
It runs **without KV/D1** (they are optional).

## What you get
- Cloudflare Worker with Hono (API: `/`, `/api/hello`, `/healthz`, `/auth/login`, `/__bootstrap`)
- Optional KV and D1 bindings (if you add them later)
- Next.js web app shell (can be deployed to Cloudflare Pages later)

## Deploy (no laptop required)
1. Push this repo to GitHub (you can upload ZIP via GitHub mobile web).
2. Open **Cloudflare Dashboard** → **Workers & Pages** → **Create** → **Worker** → **Connect to Git**,
   pick this repo, keep defaults.
3. Ensure `wrangler.toml` path is at repo root (it is). Deploy.
4. Visit `/api/hello` to verify: `https://<your-worker-subdomain>.workers.dev/api/hello`

### Optional (bind KV/D1 later)
- Add KV namespaces (KV_SESS, KV_CACHE) and D1 database (DB) in Dashboard, then
  uncomment the bindings in `wrangler.toml` and redeploy.
- Hitting `/__bootstrap` will store an admin stub into KV if bound.

## Local Dev (optional)
- Requires Node 18+ and `pnpm`. Copy `.dev.vars.example` to `.dev.vars`.
- `pnpm i && pnpm --filter @libretv/worker dev`

## API
- `GET /` → status and which bindings are enabled
- `GET /healthz` → health check
- `GET /api/hello` → sample JSON
- `POST /auth/login` → `{ email, password }` matches env (`ADMIN_EMAIL`, `ADMIN_PASSWORD`)
- `GET /__bootstrap` → writes admin JSON into KV if KV_SESS is bound
