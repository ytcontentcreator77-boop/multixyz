# Multi-provider SMM Telegram Mini App

A white-label Telegram Mini App and bot for selling social-media services through multiple standard SMM v2 API providers. The admin connects providers, imports services, configures prices and branding, and manages orders from the built-in admin panel.

## Features

- Telegram Mini App customer storefront, wallet, orders and profile.
- Owner-only admin dashboard, user/order management, price rules and branding.
- Multiple standard SMM v2 providers (API URL + key), service import by provider/category/platform, and per-order provider routing.
- Scheduled provider order status checks; provider cancellation and refill where supported.
- Admin configuration for service/category icons, currencies and payment methods.
- Editable bot message templates for welcome, order lifecycle, top-ups, refunds, help and referrals.
- Telegram Stars top-ups (the only fully implemented live payment flow).
- Cloudflare Workers + D1 deployment.

## Requirements

- Node.js 24 or newer
- A Telegram bot token from [@BotFather](https://t.me/BotFather)
- A Cloudflare account with Workers and D1 enabled
- One or more providers that implement the common SMM v2 `key` + `action` API

## Local setup

1. Install dependencies with `npm ci`.
2. Copy `.dev.vars.example` to `.dev.vars` and set `BOT_TOKEN`.
3. Run `npm run dev`.
4. Open the local setup page, enter the bot token, and complete the Telegram setup steps.
5. Claim the owner account, open the Admin page in Telegram, and connect providers under **Providers**.
6. Import services by selecting a provider, category, platform and services.

## Cloudflare deployment

1. Deploy the project to Cloudflare Workers.
2. Add `BOT_TOKEN` as a Worker secret. Optionally add comma-separated `OWNER_IDS` as a variable to pre-authorize admins.
3. Deploy the Worker and open its URL to complete the Telegram setup wizard.
4. Claim the owner account, then connect supplier API endpoints and keys from **Admin → Providers**.
5. Apply migrations with `npm run db:migrate:remote` if your deployment process does not apply them automatically.

Provider keys are stored server-side and masked in admin responses. Never share the `.dev.vars` file or provider credentials.

## Checks

```sh
npm run typecheck
npm test
npm run build
```

See [IMPLEMENTATION_STATUS.md](./IMPLEMENTATION_STATUS.md) for what is implemented and what remains intentionally unfinished.
