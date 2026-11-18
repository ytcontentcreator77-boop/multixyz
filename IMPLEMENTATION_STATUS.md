# Implementation status

## Included in this update

- Generic standard-SMM-API provider add, edit, enable/disable and removal controls.
- Provider catalog import with category selection, platform selection, service search and multi-select import.
- Imported-service order routing and scheduled status polling.
- Provider cancellation and refill actions for imported orders when the provider advertises those capabilities.
- Admin pages for provider services, service/category icons, currency rates, payment-method configuration and editable Telegram bot message templates.
- Message overrides for welcome, order lifecycle, refunds, top-ups, help and referral messages. Blank fields use built-in translated defaults.
- First-run setup no longer asks for a single supplier's API key; connect suppliers in Admin → Providers after setup.
- Legacy provider-specific catalogue sync and provider-balance alert are disabled. Existing legacy services are disabled by migration `0018_provider_first.sql`.
- Professional responsive styles for the new admin screens; existing customer UI and theme system are preserved.

## Not included / needs a separate implementation

- Non-Stars payment checkout and payment verification (UPI, Paytm, eSewa, Khalti, bank transfer, bKash, Binance and crypto). The admin screen clearly warns that enabling a method only saves its configuration; it does not create a live gateway.
- Customer top-up method/currency checkout. The existing Telegram Stars top-up remains the only live customer top-up.
- Automatic cheapest-provider selection per category and provider price refresh scheduling. Imported services can be re-imported to update them; there is no automated cross-provider price optimizer yet.
- Full visual redesign of every customer screen. Existing customer screens and styles are retained; the new admin pages use a consistent responsive card layout.
- Full removal of the old internal adapter code. It remains isolated for historical provider_id=0 order compatibility, but its branding and key setup are removed from the visible app flow.

## Validation

- All SQL migrations were applied to an in-memory SQLite database successfully.
- All TypeScript/TSX source files passed TypeScript parser syntax checks.
- Full typecheck, unit tests and production build were not run because dependencies are not installed in this environment. Run `npm ci`, then `npm run typecheck && npm test && npm run build` before deployment.
