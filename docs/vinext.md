# vinext

> ⚠️ NOT standard Next.js. APIs, conventions, file structure may differ from training data. Read `node_modules/next/dist/docs/` before writing code. Heed deprecation notices.

## What is vinext

`vinext` — experimental runtime running Next.js 16 on Vite instead of webpack, enabling Cloudflare Workers deployment for Next.js App Router apps.

## Key differences from standard Next.js

| Area | Standard Next.js | vinext |
|------|-----------------|--------|
| Build tool | webpack | Vite 8 |
| Deploy target | Node.js / Vercel | Cloudflare Workers (edge only) |
| Primary config | `next.config.ts` | `vite.config.ts` |
| RSC | built-in | `@vitejs/plugin-rsc` |
| Image optimization | `next/image` pipeline | Cloudflare Images binding |

## Do NOT

- Assume webpack-specific config or plugins are compatible
- Use `next/image` without verifying Cloudflare Images binding is configured
- Import from `next/headers`, `next/cache`, or other Next.js internals without checking vinext compatibility first
- Default to `"use client"` — prefer Server Components

## RSC

RSC provided by `@vitejs/plugin-rsc`, not Next.js internals. Verify behavior against vinext docs if differs from expectations.

## Reference

`node_modules/next/dist/docs/`
