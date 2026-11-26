# Check Electricity Web Bill Online

A free, independent guide + bill-checker front-end for Pakistani electricity consumers.
Visitors pick their distribution company (DISCO), enter a 14-digit reference number or
10-digit customer ID, and their bill opens on the OFFICIAL PITC website (bill.pitc.com.pk).

Live URL: https://check-electricity-web-bill-online.netlify.app

This site is NOT official and must never claim to be affiliated with PITC or any DISCO.
Every page footer carries the non-affiliation line.

## Files

- `index.html` — homepage: hero, company search + 11 DISCO cards (+ K-Electric card), how it works, FAQ
- `lesco-bill.html`, `gepco-bill.html`, `fesco-bill.html`, `iesco-bill.html`, `mepco-bill.html`,
  `pesco-bill.html`, `hazeco-bill.html`, `hesco-bill.html`, `sepco-bill.html`, `qesco-bill.html`,
  `tesco-bill.html` — one bill-check page per DISCO, each with the checker form
- `about.html`, `contact.html` (Netlify Forms), `privacy-policy.html`, `disclaimer.html`
- `sitemap.xml` (16 URLs), `robots.txt`
- All CSS is inlined in each HTML file; there are no external resources.

## PITC URL pattern — current (updated 2026-11-22)

The checker builds official PITC links from one config at the top of each DISCO page's script
(line ~208 in each `*-bill.html`):

```js
const PITC = { refUrl: n => PITC.discoPage + "/general?refno=" + n, discoPage: "https://bill.pitc.com.pk/gepcobill" };
```

- Reference Number mode opens `https://bill.pitc.com.pk/<disco>bill/general?refno=<14 digits>`
  (direct bill view — changed 2026-11-22 after Malik's GEPCO test failed on the old
  `gbill.aspx?refno=` pattern and the interim `/<disco>bill?refno=` landed on PITC's form page;
  Malik asked for the bill to open directly).
- Customer ID mode opens the DISCO's official PITC page: `https://bill.pitc.com.pk/<shortname>bill`
  (iescobill, lescobill, fescobill, gepcobill, mepcobill, pescobill, hazecobill, hescobill,
  sepcobill, qescobill, tescobill).

**Still to confirm end-to-end from Pakistan:** Malik re-tests a real GEPCO (and ideally IESCO)
bill number on the live site. PITC blocks embedding and times out from non-PK/datacenter
connections, so the bill always opens on PITC's own domain in a new tab. If PITC changes its
URLs later, update the `PITC` config in all 11 DISCO pages the same way.

Note: iescobill.net's checker (bill/disco.php via wrapping snippet) still uses the old
`gbill.aspx?refno=` / `ibill.aspx?refno=` pattern (observed 2026-11-22). If Malik's IESCO test
there also fails, apply the same `/iescobill/general?refno=` fix via the snippet.

Validation (in the browser, nothing is stored): spaces and dashes are stripped; digits only;
reference number must be exactly 14 digits; customer ID must be exactly 10 digits. Invalid
input shows an inline error and opens nothing.

## How to update

1. Edit the HTML file(s) in this folder.
2. Rebuild the deploy zip with files at the zip ROOT (exclude this README if you like).
3. Deploy to the Netlify site `check-electricity-web-bill-online` (production).
4. After deploying, open the live homepage and one DISCO page and re-test the checker:
   a valid 14-digit reference number should open the PITC bill; a 13-digit number should
   show an error and open nothing.

## Connecting a custom domain later

1. Buy the domain and add it in Netlify (Site settings → Domain management); enable free SSL
   and set the domain as primary.
2. Find-and-replace `https://check-electricity-web-bill-online.netlify.app` with `https://your-domain.com` in every HTML file
   (canonical tags) and in `sitemap.xml` and `robots.txt`.
3. Redeploy, then verify a canonical tag and the sitemap on the live domain.
4. Create a NEW Google Search Console property for the domain (old property data does not
   transfer) and submit the new sitemap. The Google Analytics property can stay the same.
