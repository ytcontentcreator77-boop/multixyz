# Security notes

- **Secrets stay server-side.** Telegram bot credentials and supplier API keys must be stored as Worker secrets or in the private D1 settings/provider tables. Provider API keys are masked in admin responses and must never be sent to customer screens.
- **Admin APIs are owner-only.** Every admin endpoint verifies the Telegram user against the configured owner list.
- **Provider endpoints use HTTPS.** Local/private address literals are rejected before requests are sent. Use only trusted provider endpoints and rotate a key immediately if it is exposed.
- **Payment credentials are sensitive.** Do not enable a payment method for real customer use until a gateway implementation verifies payment server-side. The current payment-method page stores configuration only; Telegram Stars is the only live payment method.
- **Webhook and Telegram tokens are private.** Do not commit `.dev.vars`, provider keys, bot tokens or deployment secrets.
- **Database changes are versioned.** Migrations are applied in order and are safe to rerun through the migration registry.
