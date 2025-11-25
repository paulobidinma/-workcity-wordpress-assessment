## Troubleshooting: New Workcity brand site not indexing after sitemap submission

When a newly-launched Workcity brand website doesn't index even after submitting the sitemap, follow a clear, ordered troubleshooting plan. Use the checks below (starting from basic crawlability) so you can quickly identify the cause and act.

---

## 1) Quick sanity checks (do these first)

- Use search operators to confirm indexing status: `site:yourdomain.com` and `site:yourdomain.com "page-title-or-unique-text"`.
- Try the canonical URL in a private/incognito browser and check HTTP headers for 200 responses.
- Verify the sitemap URL is accessible in a browser and returns 200 (e.g., `https://example.com/sitemap.xml`).

If `site:` returns no results, proceed with the deeper checks below.

---

## 2) Crawlability tests

- Check HTTP status codes for the page and any key resources (CSS/JS/images):

  - PowerShell example:

    ```powershell
    Invoke-WebRequest -Uri "https://example.com/page" -UseBasicParsing | Select-Object StatusCode
    ```

  - curl (if available):

    ```bash
    curl -I https://example.com/page
    ```

- Confirm Googlebot can access the page: use server logs to look for Googlebot user agents requesting the URL (or use GSC Crawl Stats to see recent crawl activity).
- Test fetch & render (URL Inspection → 'Test live URL' in Search Console) to confirm Google can render the page the same way a real browser does.
- Check blocking by firewall, WAF, or IP restrictions that could block Googlebot (some managed hosting or security appliances block unknown agents).

Key results to look for: 200 OK for the canonical URL, resources load without being blocked, and fetch+render shows expected content.

---

## 3) Canonical checks

- Confirm the URL you want indexed is the canonical (check for a `rel="canonical"` tag in the page head). Ensure it points to the same scheme/domain (https vs http, www vs non‑www) and not to a different location.
- Use the URL Inspection tool in Search Console — it shows which URL Google treats as canonical and whether Google selected a different canonical than yours.
- Search for duplicate pages or near-duplicate content with different URLs that might cause Google to pick another canonical.
- If using hreflang, confirm the hreflang tags are correct and consistent across language mirrors — wrong hreflang can cause Google to ignore pages for certain regions.

Common problems: canonical points to homepage or a different path; canonical URLs return non-200 responses; inconsistent canonicalization across HTTP/HTTPS or trailing slash differences.

---

## 4) Robots.txt & no-index audit

- Check `robots.txt` at `https://yourdomain.com/robots.txt` for Disallow rules or syntax errors (and test with Search Console's robots.txt tester).
- Inspect meta robots on the page source. For example, a meta tag like ``<meta name="robots" content="noindex">`` will prevent indexing — also check for `X-Robots-Tag` headers in server responses (these can block pages via HTTP headers).
- Confirm user-agent specific rules aren't unintentionally blocking Googlebot or generic bots.
- Verify that your server or deployment scripts did not accidentally add a noindex header/site-wide (some build or staging systems add noindex by default).

### Useful quick tests

Get robots file (PowerShell):

```powershell
Invoke-WebRequest -Uri "https://example.com/robots.txt" -UseBasicParsing | Select-Object -ExpandProperty Content
```

Check headers (curl):

```bash
curl -I https://example.com/page   # look for X-Robots-Tag in response headers
```

---

## 5) Sitemap structure issues to audit

- Confirm the sitemap uses canonical URLs only (no URLs that 301/302 redirect, no non-canonical variants, no URLs blocked by robots.txt).
- Ensure the sitemap is accessible and valid XML (no parse errors). Use tools like the Search Console Sitemaps report or online XML validators.
- Make sure the sitemap contains only URLs that return 200 and are indexable (not noindex). Remove URLs returning 4xx/5xx or those that redirect.
- Check lastmod timestamps — don't rely solely on outdated or incorrect lastmod values; lastmod doesn't force reindexing.
- Large sitemaps: break into sitemap index + multiple sitemaps to avoid size limits (max ~50,000 URLs per sitemap and 50MB uncompressed). Compress with .gz if needed.

Problems to look for: sitemap referencing staging URLs, non-canonical URLs, or blocked/redirecting URLs — all of these reduce sitemap utility.

---

## 6) Page speed / JavaScript and indexing blockers

- Check if the rendered HTML that Google sees contains meaningful content. If the site relies on heavy client-side JS to populate text, Google may not index correctly if rendering fails.
- Use "Test live URL" in Search Console and the Mobile-Friendly test to capture how Google renders pages; compare source HTML to rendered DOM.
- Large/slow JavaScript bundles and render-blocking resources can cause Google to delay or fail rendering, which affects indexing; reduce critical JS, use server-side rendering (SSR) or pre-rendering for important landing pages.
- Reduce heavy third‑party scripts and excessive time-to-first-byte (TTFB) delays. Improving LCP/INP and removing long main-thread tasks helps both user experience and indexing speed.

When JS is the issue, solutions include server‑side rendering, dynamic rendering for bots, or generating static HTML for crucial pages.

---

## 7) Search Console debugging steps (detailed)

### URL Inspection — live test

- Paste the full URL into Search Console → URL Inspection.
- Click 'Test live URL' to see current crawlability and rendering status and potential issues (blocked resources, 4xx/5xx responses, canonical decisions).
- If it returns OK and is indexable, click 'Request indexing'. Note that Request Indexing doesn't guarantee immediate indexing — it requeues the URL for crawl.

### Coverage report

- Look at Coverage → Errors, Excluded, Valid. Common statuses for newly submitted URLs: "Discovered – currently not indexed" or "Crawled – currently not indexed".
- For exclusion reasons, Search Console explains whether it's blocked by robots.txt, duplicate without user-selected canonical, or has a noindex.

### Sitemaps report

- Check that the sitemap was successfully submitted, the number of discovered URLs matches expectation, and review any warnings or errors (parsing errors, blocked entries).

### Mobile Usability & Core Web Vitals

- Check these reports for issues that may cause poor rendering or prevent correct indexing.

### Test URLs in other tools

- Mobile-Friendly Test and Rich Results Test can reveal rendering and structured data problems.

### Crawl Stats & Server Logs

- Compare Search Console Crawl Stats with your server logs to confirm Googlebot requests and find any 4xx/5xx events or long pauses in response.

### Check for manual actions or security issues

- On rare occasions, a manual action or security issue will affect indexing; inspect those messages in GSC.

---

## 8) Additional practical checks & fixes (prioritized)

1. Remove accidental noindex and fix robots.txt if needed.
2. Ensure canonical tag points to the correct canonical URL and returns 200.
3. Fix server errors and ensure pages load quickly and consistently.
4. Ensure sitemap only lists canonical, 200-indexable pages and re-submit.
5. Improve internal linking and add a few high-quality external links to new pages to help discovery.
6. If heavy JS, provide SSR or prerendered HTML for landing pages.
7. After fixes, use URL Inspection → Test live URL → Request indexing and monitor coverage changes.

---

## 9) Logging and support steps

- Check server logs (or ask hosting / DevOps) to trace Googlebot requests and any 403/401 or 5xx responses.
- If GSC states "Denied due to robots.txt" but robots.txt looks OK, verify host-level firewalls or security services (Cloudflare, Akamai, Sucuri) are not blocking Googlebot IPs.
- If the site was previously on a different domain or under canonical cross links, ensure there are no residual canonical signals pointing to the old domain.

---

## 10) When to escalate

- If your pages are still not indexed after fixing robots/noindex/canonical issues and requesting indexing: gather:
  - screenshots of URL Inspection tests
  - server logs showing Googlebot requests
  - list of recent sitemap submissions and Search Console messages
  - timeline of changes you made

- With these, involve platform hosting support or Google Search Console help forums. If a hosting-layer block or security service is the root cause, host support can help whitelist Googlebot or correct the configuration.

---

## Quick checklist (copy and run)

- [ ] site:yourdomain.com returns expected pages
- [ ] Canonical resolved and self-referential
- [ ] Page returns 200 and renders expected content
- [ ] No global or page-level noindex meta or X-Robots-Tag
- [ ] robots.txt accessible and not blocking Googlebot
- [ ] Sitemap accessible, valid XML, lists only 200 canonical URLs
- [ ] No 4xx/5xx on key pages; no 301 loops for canonical URLs
- [ ] URL Inspection > Test live URL OK and Request indexing performed
- [ ] Server logs confirm Googlebot crawling

---

If you want, I can now:

- produce a printable checklist for your engineers, or
- run a simulated checklist on a specific URL if you give me the domain (or sample responses) so I can help interpret the results.

