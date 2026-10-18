# scraper-sample: a polite, tested web scraper with clean CSV/Excel output

> A Python scraper for a scraping-practice site: it follows pagination, fetches 1,000 detail pages and writes clean CSV and Excel files with a run report and an error log. It checks robots.txt, waits between requests, retries transient errors, validates every record and keeps going when a page fails. 21 offline tests cover parsing, retries, rate limiting and exports. Built with AI coding assistants under my direction; I review and test everything.

**The goal.** Show how I build scrapers that a client can trust: the data is clean, the run is repeatable, the site is not hammered, and failures are visible instead of silent.

**The target.** [books.toscrape.com](https://books.toscrape.com), a sandbox site made for scraping practice. No real business or personal data is involved.

**What the scraper does.**
- Follows the pagination (50 listing pages) and opens each book page (1,000 pages) to collect UPC, category, price with and without tax, stock count, reviews and description.
- Checks `robots.txt` before every URL, waits between requests, retries 429/5xx and connection errors with backoff (honouring `Retry-After`), and can cache raw HTML so reruns do not touch the site again.
- Validates every record. Bad records go to an error log, not to the dataset. One failing page never stops the run.
- Writes `books.csv`, a formatted `books.xlsx` (filters, frozen header, £ formatting, a run-summary sheet), `errors.csv` when there are errors, a JSON run report and a timestamped log.

**Result of the sample run.**

Full run on 2026-10-18: 50 listing pages and 1,000 detail pages in 515 seconds (about 8.6 minutes) at 0.5 seconds between requests. 1,000 books with 1,000 distinct UPCs, 50 categories, prices from £10.00 to £59.99, and 0 errors. The only empty fields are two descriptions that do not exist on the site itself.

**How I know it works.** 21 automated tests, all offline (saved pages and a fake HTTP session): parsing, robots.txt rules, the rate limit, retries with backoff, `Retry-After`, giving up after the retry limit, the cache, a failed page not stopping the run, record validation and the CSV/Excel writers. The parser raises an error when a page has an unexpected layout, instead of returning empty fields.

**What I do not do.** I do not bypass CAPTCHAs or anti-bot systems, collect personal data without a legal basis, or scrape sites whose terms forbid it. The scraper's user agent says what it is.

**How it was built.** With AI coding assistants (Claude Code) under my direction. I define the requirements and the rules above, review the code and the data, and answer for the result.

**Limits.** Static HTML only (JavaScript-rendered sites need a browser-based approach). Built for one practice site; adapting it to a client's site starts with reading that site's terms and robots.txt.

**What a client can hire from this.** A scraper for a public website you are allowed to collect from, delivered with the script, the data, a run report, an error log and tests, plus a clear answer if scraping that site is not allowed.

---

Code: [github.com/SetsuroID/scraper-sample](https://github.com/SetsuroID/scraper-sample). The data comes from a practice site built for scraping; nothing here targets real businesses or personal data.

[Back to profile](../README.md)
