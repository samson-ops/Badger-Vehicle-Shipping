# Badger Vehicle Shipping — SEO & Google-compliance audit (Oct 12, 2026)

Scope: all 29 pages in this folder. Tools: custom crawler (titles, metas, headings, canonicals, schema, links, images, duplicate content), Google Lighthouse 13.5 (SEO, Accessibility, Best Practices), Playwright render at 1366px and 400px.

## Results after fixes
| Check | Result |
|---|---|
| Lighthouse SEO | 100 / 100 on every page type tested (home, service, location, guide) |
| Lighthouse Accessibility | 100 / 100 |
| Lighthouse Best Practices | 96 / 100 (only "errors in console", caused by the audit sandbox blocking Google Fonts/Maps; not reproducible live) |
| Titles | All ≤ 60 chars, unique, keyword-first, brand suffix |
| Meta descriptions | All 70–155 chars, unique |
| H1 | Exactly one per page; H1 → H2 → H3 order correct (hidden H2 added above the quote widget so its H3 no longer skips a level) |
| Canonical / lang / viewport / robots | Present on every page; 404 is noindex |
| Structured data | Valid JSON-LD on every page: Organization (home), LocalBusiness + geo (8 offices), Service (8 services), BreadcrumbList (all), FAQPage (where FAQs exist) |
| Internal links | 0 broken; every page reachable from nav + footer; breadcrumbs on all subpages |
| Images | All have alt text; logo served as WebP (21 KB, was 199 KB PNG) with width/height to prevent layout shift; lazy-loaded below the fold; proper 32px favicon + Apple touch icon |
| Mobile | No horizontal overflow at 400px on any page tested; tap targets pass |
| Phone/email links | Rendered into the HTML at build time (previously filled only by JavaScript), so crawlers see real numbers |
| Duplicate content | Location pages de-templated: shared service grid and 3-step block replaced with unique per-city copy; generic FAQs dropped. Body-text similarity between any two office pages now 0.45–0.66 (was 0.67–0.80). Each office page carries 1,075–1,150 words of unique body copy |
| Third-party references | Quote widget's static HTML now says "Badger Vehicle Shipping" and links to badgervehicleshipping.com (previously defaulted to Ship Guy until JS ran) |
| Sitemap / robots | sitemap.xml with all 29 URLs; robots.txt allows all and points to the sitemap |
| Security headers | `_headers` adds nosniff, frame, referrer and permissions policies; 1-year immutable cache on /assets |

## Google policy risk review
1. **Virtual-office addresses (the biggest real risk).** Several office addresses are suite/box numbers at shared-office or mailbox locations (e.g. "#139", "#480", "Suite 133"). Google Business Profile guidelines prohibit listings at virtual offices or mailboxes unless staffed during business hours. The website itself is fine, but if the matching GBP listings are not staffed locations, Google can suspend them, and a suspended GBP undercuts the location pages. Make sure each listed office is one you can defend as a real, staffed location, or at minimum keep the GBP name/address/phone exactly consistent with these pages.
2. **Doorway-page guidance.** Google penalizes near-identical city pages that exist only to rank. These pages now have substantial unique local content (corridors, employers, neighborhoods, routes, local pricing notes) and a real address, phone and map each, which is the accepted pattern for genuine multi-office businesses. Keep it that way: do not spin up additional city pages without a real office.
3. **FAQ rich results.** Since August 2023 Google only shows FAQ rich snippets for government and health sites. The FAQPage schema is harmless and still helps understanding, but do not expect visible FAQ snippets.
4. **Claims.** No invented reviews, ratings, review counts or customer names anywhere on the site. "Licensed & bonded" and "100% insured" are stated as broker/carrier facts; the Licensing page explains them. MC/USDOT numbers are omitted at your request; adding them to the Licensing page and footer would strengthen trust signals and is standard for FMCSA brokers.
5. **SMS consent (TCPA).** The quote form's consent checkbox, the consent sentence, and the Privacy Policy SMS section are in place and aligned. Keep the checkbox unchecked by default (it is).
6. **Third-party keys.** The Google Maps Places key inside the quote widget belongs to the Ship Guy account; add www.badgervehicleshipping.com to its HTTP-referrer restrictions or swap in a Badger key, or ZIP autocomplete will silently fail.

## Still to do after launch (cannot be done from files)
- Add the site to Google Search Console (DNS or HTML-tag verification), submit sitemap.xml, request indexing on the homepage and /locations/.
- Create/claim a Google Business Profile for each office with name, address and phone matching the office page exactly, and link each GBP to its /locations/ page.
- Add real customer reviews (a reviews section is ready to be added; I will not fabricate any).
- Add one or two real photographs (trucks, deliveries); Google favors pages with original images and the site currently has only the logo.
- Set up Google Analytics 4 / Tag Manager if wanted (not included; nothing is tracking visitors yet).
- Confirm the lead proxy works on the live domain: submit a test quote, check it lands in BeRocker under "Badger Vehicle Shipping".

## Known non-issues
- The quote widget's own markup begins with an H3; a visually-hidden H2 precedes it so heading order passes.
- The string `YOUR_LEAD_SOURCE_KEY` appears inside the widget's JavaScript as a safety check; it is not visible and not a leak.
- Cost ranges on /car-shipping-cost/ are typical market ranges; verify against your pricing engine's actual output on those lanes.
