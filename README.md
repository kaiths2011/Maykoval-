# MAYKOVAL — Shopify storefront

All products, prices, variants, images, stock, discounts and collections come live from Shopify. No products are hardcoded.
Files: `index.html` (storefront) · `api/shopify.js` (secure server proxy) · `package.json`.
Your token lives ONLY in server environment variables; it is never in the browser code.

## 1. Shopify setup (once)
1. Shopify Admin → **Settings → Apps and sales channels → Develop apps** → *Allow custom app development* → **Create an app** ("MAYKOVAL Storefront").
2. **Configuration → Storefront API integration → Configure**. Tick:
   `unauthenticated_read_product_listings`, `unauthenticated_read_product_inventory`, `unauthenticated_read_product_tags`,
   `unauthenticated_read_collection_listings`, `unauthenticated_write_checkouts`, `unauthenticated_read_checkouts`. Save.
3. **Install app**, then open **API credentials** and copy the **Storefront API access token**.
4. Make sure products and collections are **published to the Online Store** sales channel (Products → product → Sales channels).
5. Create collections: Personal Care, Health Care, Hair Care, Massagers, Smart Lifestyle Gadgets. They appear automatically as categories and in the menu.
   - Optional collection named **Featured** (handle `featured`) fills the Featured row.
   - Optional product metafield `custom.specifications` (multi-line text) shows a Specifications block.
   - A "Compare-at price" on a product/variant shows as a sale price.

## 2. Deploy (Vercel, free)
1. Put this folder in a GitHub repo → vercel.com → **Add New Project** → import it (no build settings needed).
2. **Settings → Environment Variables**:
   - `SHOPIFY_STORE_DOMAIN` = `your-store.myshopify.com`
   - `SHOPIFY_STOREFRONT_TOKEN` = the token from step 3
3. Deploy. Add your own domain under Settings → Domains.

Local test: `npx vercel dev` (create a `.env` with the two variables above).

## 3. Before launch
- Edit `CFG` at the top of the script in `index.html`: social links, support email, reviews (empty = section hidden; use real reviews only).
- Replace the Shipping / Returns / Contact text, or link to Shopify's policy pages.
- Place a test order; it appears in Shopify Admin → Orders. Checkout is Shopify's secure hosted checkout.
- Newsletter signups arrive in Shopify Admin → Customers (tag `newsletter`).
