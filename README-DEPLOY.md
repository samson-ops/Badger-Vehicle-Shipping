# Badger Vehicle Shipping — website

Deploy this folder as-is to Cloudflare Pages (site root = this folder).

## Pages
- `/services/` hub + 8 service pages (open, enclosed, door-to-door, expedited, snowbird, military, state-to-state, auction)
- `/how-it-works/`, `/car-shipping-cost/`, `/car-shipping-checklist/`, `/cross-country-car-shipping/`, `/faq/`, `/contact/`, `/about/`
- `/privacy/`, `/terms/`, `/licensing/` — legal pages (review wording with your attorney/compliance before launch)
- `404.html` — Cloudflare Pages serves it automatically; `_redirects` maps the old `/privacy` style links
- `/` — homepage (`index.html`)
- `/locations/` — hub page listing the eight Wisconsin offices
- `/locations/<city>-wi/` for green-bay, eau-claire, kenosha, oshkosh, fond-du-lac, madison, waukesha, janesville — SEO location pages (unique copy, local phone, address, Google Map, LocalBusiness + FAQ + Breadcrumb schema, quote tool)
- `sitemap.xml`, `robots.txt` — submit the sitemap in Google Search Console after deploy

## Lead tracking
- `functions/api/quote/[[path]].js` — lead proxy. The Badger BeRocker Lead Source key (`6ac9335160415`) is set as DEFAULT_KEY. Preferred: set env var `BEROCKER_LEAD_KEY` in Cloudflare → Pages → Settings → Environment variables.
- Each page tags its leads: `BADGER-WEB-…` (homepage) and `BADGER-<CITY>-WEB-…` (e.g. `BADGER-MADISON-WEB-…`, `BADGER-FONDDULAC-WEB-…`) so you can see which office page produced the lead.

## Phone numbers (already set)
- Main: (608) 420-2685 — homepage and locations hub
- Green Bay (920) 678-7550 · Eau Claire (715) 999-7030 · Kenosha (262) 360-6577 · Oshkosh (920) 824-3407 · Fond du Lac (920) 638-6732 · Madison (608) 420-2685 · Waukesha (262) 384-6890 · Janesville (608) 401-4120 — each office page uses its own number everywhere, including inside the quote tool.

## Before going live
1. Confirm the email `info@badgervehicleshipping.com` (set in `window.SITE` near the bottom of each page).
2. Google Maps key: add `www.badgervehicleshipping.com` to the key's referrer restrictions, or paste a new key into `PQ_CONFIG.googleMapsKey` (ZIP suggestions only; the tool works without it).
3. Footer links `/privacy`, `/terms`, `/licensing` need pages.
4. Google Business Profiles: make sure each office's name, address and phone match the pages exactly (NAP consistency).

## Test after deploy
- Submit a quote from the homepage and from one office page → both leads land in BeRocker under **Badger Vehicle Shipping**, with the secondary_id prefixes above.
- Open each `/locations/...` page on a phone: map loads, local number shows in header, footer and quote tool.
