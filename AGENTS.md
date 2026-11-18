# Multi-provider Telegram SMM Mini App

- Stack: Preact + Vite (`src/`), Hono on Cloudflare Workers (`worker/`), D1 (`migrations/`). One Worker serves the app, API and Telegram webhook.
- Keep Cloudflare free-plan limits in mind: low CPU, bounded subrequests and batched D1 writes.
- New supplier connections use the standard SMM v2 `key + action` API through `worker/providers.ts`. API keys are stored server-side and masked in admin responses. New imported services have `provider_id > 0`; order placement, status polling, cancellation and refill route through that provider.
- Admins connect providers in Admin → Providers, then import services by category and platform. Imported services are enabled when imported. The legacy built-in catalogue sync is disabled by default; migration `0018_provider_first.sql` disables legacy `provider_id = 0` services.
- A small legacy adapter remains in `worker/notpanel.ts` for compatibility with historical `provider_id = 0` orders and data. Do not use it for new services or expose its old branding in the UI.
- Money remains integer micro-USD in balances, ledger, charges, refunds and costs. Telegram Stars remains the only fully implemented live payment flow. Currency and payment-method records are configurable, but non-Stars checkout and gateway verification are not yet implemented.
- User-facing text is white-label and uses `{brand}` where appropriate. Bot message overrides are stored in `settings.bot_messages`; blank templates fall back to translated defaults.
- Admin API routes are owner-only. Provider API keys and payment credentials must never be returned to the client.
- Checks: `npm run typecheck && npm test && npm run build`. Dependencies are not included in this source archive; install from `package-lock.json` before running these checks.
