# Coccinelle Supermarket: storefront and staff console prototype

A single-file prototype (`index.html`, no build step) of the Coccinelle AI Commerce & Marketing Control Center.
Everything runs in the browser against sample data. There is no real backend, payment, WhatsApp or social posting.

## What works in the prototype

**Storefront**: home page, shop and offers pages with search and category filters, wishlist, cart, three-step checkout
(details, review, explicit confirmation), delivery or pickup, card (sandbox) or bank transfer. No cash on delivery.

**Order rules (simulated server)**: totals are recalculated from the catalogue, unique order numbers (`CC-YYMMDD-0001`),
duplicate confirmations return the same order, price changes before confirmation are flagged, out-of-stock items are refused.

**15-minute delivery rule**: timer starts on delivery orders. On timeout the customer is offered pickup and nothing changes
until they agree. Decline or no reply keeps the order pending and alerts staff. Use "Test tool: skip 15 minutes" in the staff order view.

**Shopping assistant ("Coco")**: English and basic Arabic, uses catalogue data only, one upsell then respects a refusal,
hands off complaints, refunds and unknown products to staff, never confirms an order itself.

**Staff console**: six roles with different permissions (denied actions are logged), offers with draft / pending /
approved states, edit-after-approval resets approval, manual stock status, campaign preview with the fixed poster template and
caption, simulated 09:00 Asia/Dubai run, payment verification (bank transfer needs a reference and a bank check), audit log.

## Not real yet (needs the plan's later phases)

Real auth and database row-level security, real payments, Meta publishing, WhatsApp Business Platform, real AI provider,
Make.com scenarios, persistent storage. Contact details and the delivery fee (AED 8, free over AED 100) are sample values.
Do not enter real customer data.

## Publish it free with GitHub Pages

1. Create a GitHub repository, for example `coccinelle-web`.
2. Upload `index.html` and `README.md` to the repository root (or `git add . && git commit -m "Prototype" && git push`).
3. Repository **Settings > Pages**, set **Source** to "Deploy from a branch", branch `main`, folder `/ (root)`, then Save.
4. After about a minute the site is at `https://<your-username>.github.io/coccinelle-web/`.

## Or Cloudflare Pages (also free)

1. Cloudflare dashboard > **Workers & Pages** > **Create** > **Pages** > connect the GitHub repository.
2. Framework preset: **None**. Build command: empty. Output directory: `/`.
3. Deploy. You get a `*.pages.dev` address. Recheck current free limits at the links in the project plan.

## Deep links

`#shop`, `#offers` and `#staff` open those views on load.

## Design tokens (for rebuilding in Figma)

| Token | Light | Dark |
|---|---|---|
| Background | `#F3F8EE` | `#0E1A12` |
| Surface | `#FFFFFF` | `#16261B` |
| Ink | `#14261A` | `#E7F2E4` |
| Brand green | `#2F7D32` | `#58B85C` |
| Brand red (calls to action) | `#E0262B` | `#EF4A4F` |
| Leaf tint | `#E3F0D4` | `#1E3524` |
| Footer | `#1F5C2A` | `#0B2A14` |

Fonts: Bricolage Grotesque (headings), Figtree (body), Caveat (script accents). Radius 12 to 28 px. Cards 1 px border.

## Next steps from the plan

1. Choose one backend (Cloudflare Workers or Supabase) and move the order, offer and role logic server-side with row-level security.
2. Replace the simulated payment with a UAE-eligible provider in sandbox, verified by signed webhooks.
3. Connect Facebook/Instagram test accounts through the official APIs, then the WhatsApp Business Platform.
