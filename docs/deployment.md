# Deployment

## Target

Cloudflare Workers via Wrangler. Edge runtime only — no Node.js APIs.

## Build

```bash
npm run build   # vinext build → outputs to dist/
```

## Worker entry

`worker/index.ts` — Cloudflare Worker entry point. Responsibilities:

- Image optimization at `/_vinext/image` via `IMAGES` binding
- All other requests delegated to `vinext/server/app-router-entry`

Required bindings:

| Binding | Purpose |
|---------|---------|
| `ASSETS` | Static asset fetcher |
| `IMAGES` | Cloudflare Images (image optimization) |

## Deploy

```bash
npx wrangler deploy
```

## Local preview

```bash
npx wrangler dev
```

## Notes

- `next/image` default pipeline replaced by `vinext/server/image-optimization` via Cloudflare Images
- SVG files bypass optimization endpoint by default (served directly)
- `ctx.waitUntil()` available via `getRequestExecutionContext()` for deferred background work