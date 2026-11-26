# Check Electricity Web Bill Online — Google setup pack (ready, not yet deployed)

Prepared: 2026-11-22. Site: https://check-electricity-web-bill-online.netlify.app
Status today: 16 pages live (homepage + 11 DISCO pages + About/Contact/Privacy/Disclaimer),
sitemap.xml (16 URLs) + robots.txt ready. NO Google Analytics or Search Console tags yet
(verified 2026-11-22: no gtag / verification tag in any HTML file). US Calculator Tools
already has both; this site is the only one of Malik's three without them, so Google cannot
yet be told to crawl it via sitemap and visits cannot be measured.

## Why batch this into ONE deploy (Netlify credits) — UPDATED 2026-11-22 19:32 PKT
Team "Fesco Online Bill's team" (Free, 300 credits/cycle Nov 19–Dec 18) EXHAUSTED all credits
on 2026-11-22 (Netlify emails 13:38Z 75%, 14:02Z 100%). Each production deploy costs 15 credits.
Netlify added 30 operational credits: published sites keep serving, production deploys + Agent
Runners are PAUSED, preview/branch deploys still work. If operational credits also exhaust,
sites suspend until the cycle resets on **December 18** (Netlify email 2026-11-22T14:02Z).
Malik chose to WAIT (2026-11-22 14:09Z). Cron `netlify-credits-reset-deploy` runs Sat 19 Dec
2026 13:19 PKT (after reset) for ONE deploy of the pending logo change (logo.jpg etc. ready in
this folder) — that cron does NOT do the Google steps below, which need Malik present.
Verified 2026-11-22 19:32 PKT: bill site, calculators site and iescobill.net all return HTTP 200.
So: do NOT attempt a production deploy before the reset. After reset, ONE batched deploy should
carry, together:
1. Pending logo change (already in files, cron covers it if run first — avoid a second deploy).
2. GA4 gtag on all 16 pages (new property, see below).
3. Search Console HTML-tag verification meta on homepage (or DNS/file method if Malik prefers).
4. Any checker tweak that Malik's Customer ID test (below) shows is needed.
Preview deploys are free (0 credits) — test there first, then one production deploy.

## Steps (needs Malik for Google sign-in / phone verification, as before)
1. In the existing GA account "FESCO" (fescobill1981@gmail.com): create GA4 property
   "Check Electricity Web Bill Online", Pakistan Time, PKR (or USD — Malik's choice; PKR fits
   a Pakistan-audience site). Copy the Measurement ID (G-XXXXXXXXXX). Do NOT revoke Site Kit
   access for iescobill.net — separate site, untouched.
2. Add the gtag snippet (same pattern as US Calculator Tools) to <head> of all 16 HTML files.
3. In Search Console: add URL-prefix property https://check-electricity-web-bill-online.netlify.app/
   and verify via HTML tag (add the meta tag to index.html in the same batched deploy).
   Malik completes phone verification himself if Google asks (as on 2026-11-18/19).
4. Submit sitemap: https://check-electricity-web-bill-online.netlify.app/sitemap.xml
   (expect "Success", 16 pages discovered — same sitemap route that worked for calculators).
5. Verify live: gtag present on homepage + one DISCO page; GA4 Realtime shows a visit;
   sitemap status Success. Do NOT send manual indexing requests unless Malik asks
   (quota limits hit twice on calculators; sitemap route is proven).
6. Custom domain later (Malik decides when): follow README "Connecting a custom domain
   later" — new GSC property for the domain, GA property stays.

## Before that deploy: Malik's bill tests (2 minutes, from Pakistan) — UPDATED 2026-11-22
- DONE: GEPCO 14-digit reference number → Malik confirmed 2026-11-22 13:40Z "ok ab kam kar
  raha hai". Current mechanism (gepco-bill.html line ~234): POST to
  https://bill.pitc.com.pk/gbill.aspx?refno=<14 digits>, same as iescobill.net's checker.
  Bill opens on PITC's domain in a new tab (PITC blocks embedding). Do not change this.
- PENDING: Customer ID mode (10 digits, deployed 2026-11-22 13:59Z, before credits ran out):
  POST to https://bill.pitc.com.pk/<disco>bill/general?appno=<10 digits> (pattern Malik supplied
  from PITC's own GEPCO consumer-ID URL). Malik has not yet confirmed this test. No deploy is
  needed to test it — it is already live. Ask him to report: bill / error / blank / PITC form.
- iescobill.net homepage checker still uses gbill.aspx and worked 18 Nov; Malik was asked to
  test it too. Do NOT claim it is broken. If it fails there, the fix goes into iescobill.net's
  wrapping snippet (WordPress, no Netlify credits involved).

— Chilly
