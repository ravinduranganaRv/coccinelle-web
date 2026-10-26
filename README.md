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

**Home page motion**: the paper bag tilts toward the cursor in 3D, produce floats and moves away from the pointer, bubbles rise,
and the Garden veg / Orchard fruit buttons trigger a spin and an implode-and-explode swap with a background tint change.
All of it is drawn with the site's own vector art (no 3D model files or third-party assets) and it is switched off for
visitors who prefer reduced motion.

**Staff sign in**: the staff console is locked. Each person has their own username and password (stored as salted PBKDF2
hashes, never plain text), a 5-attempt lockout, 15-minute idle sign-out, forced "choose your own password" reminder on first
sign in, and a password-change dialog.

**Staff console** (what you see depends on your account):
- Orders, Offers and the audit trail follow the six roles in the plan; refused actions are logged.
- Offers: draft, pending, approved. Editing an approved offer resets approval. The author cannot approve their own draft.
- **Products** tab: add and edit products (SKU, name, Arabic name, category, pack size, price, stock, picture or photo),
  hide or show on the storefront. Visible only to accounts with product access, and only 3 accounts can hold it.
  Editing name, pack size or price sends a linked offer back to draft.
- **Users** tab (Super Admin only): create accounts, reset passwords (one-time temporary password), disable, change role,
  grant or remove product access.
- Campaign preview with the fixed poster template and caption, simulated 09:00 Asia/Dubai run, payment verification
  (bank transfer needs a reference and a bank check).

## Not real yet (needs the plan's later phases)

**Staff sign in is a prototype.** The site is static, so the password check runs in the visitor's browser. Anyone technical
can read or change the page code, so this keeps casual visitors out but is not real security. Accounts, password changes and
product edits are saved only in the browser that made them (localStorage), not shared between devices. Real protection needs the
backend in the plan: server-side authentication, role checks and database row-level security.

Also not real yet: real payments, Meta publishing, WhatsApp Business Platform, real AI provider,
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

## Staff accounts

Seven starting accounts are included: `owner` (Super Admin), `manager` and `deputy` (Store Managers), `marketing`,
`orders`, `payments` and `auditor`. The first three have product access. Starting passwords are not stored in the repository;
they were given to the project owner separately. Each person must choose their own at first sign in. If the owner is locked out,
clearing this site's data in the browser restores the starting accounts.

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
