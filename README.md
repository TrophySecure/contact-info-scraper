[Contact Info Scraper](https://apify.com/junipr/contact-info-scraper?fpr=data)

## What does Contact Info Scraper do?

Contact Info Scraper crawls any website and extracts all available contact information in a single run. It finds email addresses, phone numbers, physical addresses, and social media profile links (LinkedIn, Twitter/X, Facebook, Instagram, YouTube, GitHub) by intelligently crawling multiple pages on each domain. The actor automatically prioritizes contact-heavy pages like `/contact`, `/about`, `/team`, `/impressum`, and `/support` to maximize results with minimal page crawls.

Give it a list of website URLs and it returns one structured result per domain with every contact detail it finds, deduped and sorted. It is ideal for lead generation, sales prospecting, competitor research, or building business contact databases at scale.

## Features

- **Multi-signal extraction** — Emails, phone numbers, physical addresses, and social media profiles in one run
- **Smart crawling** — Automatically prioritizes contact, about, team, and support pages before general internal links
- **Six social platforms** — Detects LinkedIn, Twitter/X, Facebook, Instagram, YouTube, and GitHub profiles
- **Batch processing** — Scrape contact info from dozens or hundreds of websites simultaneously
- **Per-domain deduplication** — All results are deduplicated per domain so you get clean, unique data
- **Configurable extraction** — Toggle each extraction type on or off (emails, phones, socials, addresses)
- **Adjustable crawl depth** — Control how many pages per domain to crawl (1-100)
- **Contact page detection** — Reports the URL of the contact or about page if one was found
- **Polite crawling** — Configurable request delay and concurrency to respect target servers
- **Proxy support** — Built-in Apify proxy support for accessing any website reliably

## Input Configuration

```
{
  "urls": ["https://example.com", "https://another-site.com"],
  "maxPages": 10,
  "followLinks": true,
  "priorityPages": ["/contact", "/about", "/team", "/impressum", "/support"],
  "extractEmails": true,
  "extractPhones": true,
  "extractSocials": true,
  "extractAddresses": true,
  "maxConcurrency": 5,
  "requestDelay": 1000,
  "proxyConfiguration": { "useApifyProxy": true }
}
```

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `urls` | string[] | `["https://crawlee.dev"]` | Website URLs to scrape for contact information |
| `maxPages` | integer | `10` | Maximum pages to crawl per domain (1-100) |
| `followLinks` | boolean | `true` | Follow internal links to discover more pages |
| `priorityPages` | string[] | `["/contact", "/about", ...]` | URL paths to crawl first |
| `extractEmails` | boolean | `true` | Extract email addresses |
| `extractPhones` | boolean | `true` | Extract phone numbers |
| `extractSocials` | boolean | `true` | Extract social media profile links |
| `extractAddresses` | boolean | `true` | Extract physical addresses |
| `maxConcurrency` | integer | `5` | Maximum concurrent requests (1-20) |
| `requestDelay` | integer | `1000` | Delay between requests in milliseconds |
| `proxyConfiguration` | object | Apify proxy | Proxy settings for web requests |

## Output Format

Each domain produces one result object:

```
{
  "url": "https://example.com",
  "emails": ["info@example.com", "sales@example.com"],
  "phones": ["+1-555-123-4567"],
  "socialProfiles": {
    "linkedin": "https://linkedin.com/company/example",
    "twitter": "https://twitter.com/example",
    "facebook": "https://facebook.com/example",
    "instagram": null,
    "youtube": null,
    "github": "https://github.com/example"
  },
  "addresses": ["123 Main St, San Francisco, CA 94102"],
  "contactPageUrl": "https://example.com/contact",
  "scrapedAt": "2026-03-11T12:00:00.000Z"
}
```

## Usage Examples / Use Cases

- **Lead generation** — Build prospect lists by scraping contact info from company websites in your target market
- **Sales prospecting** — Enrich a list of company domains with emails, phone numbers, and LinkedIn pages for outreach
- **Competitor research** — Discover competitors' social media presence and contact channels across platforms
- **Business directory building** — Aggregate contact details from hundreds of local business websites
- **Due diligence** — Verify a company's public contact information and online presence before partnerships
- **Recruitment** — Find team pages and contact emails for companies you want to recruit from or sell to

## Proxy Requirements

This actor crawls arbitrary websites, some of which may block datacenter IP addresses or require geo-specific access. Proxy usage is optional but recommended for reliable results across diverse target sites.

- **Paid Apify plan users**: The default datacenter proxy configuration works for most websites. Switch to residential proxy in the input settings if you encounter blocks on specific sites.
- **Free plan users**: The actor works without proxy for many websites. If you experience access issues, provide your own proxy URL in the Proxy Configuration input field.
- Proxy is most important when scraping sites with Cloudflare protection, aggressive bot detection, or geo-restricted content.

## FAQ

### How many websites can I scrape in one run?

There is no hard limit on the number of URLs you can provide. The actor processes them in parallel based on your `maxConcurrency` setting. For large batches (100+ domains), consider increasing the timeout in your run configuration.

### What if a website has no contact information?

The actor returns a result for every input URL regardless. If no contact data is found, the `emails`, `phones`, and `addresses` arrays will be empty and `socialProfiles` values will be `null`. Check the `contactPageUrl` field — if it is `null`, the site may not have a standard contact page.

### Does it extract emails from JavaScript-rendered pages?

The actor uses Cheerio (server-side HTML parsing), which does not execute JavaScript. Emails embedded directly in HTML, `mailto:` links, and common obfuscation patterns are extracted. For heavily JavaScript-dependent sites, emails rendered only by client-side scripts may be missed.

### How does priority page crawling work?

Before following general internal links, the actor automatically queues requests for common contact page paths (`/contact`, `/about`, `/team`, `/impressum`, `/support`) on each domain. These pages are crawled first because they are most likely to contain contact information, reducing the number of pages needed to find results.

### Can I scrape only emails without phone numbers?

Yes. Set `extractPhones`, `extractSocials`, and `extractAddresses` to `false` and only `extractEmails` to `true`. The actor will still crawl the same pages but only extract and return email addresses.

## Related Actors

- [Email Validator](https://apify.com/junipr/email-validator) — Validate extracted emails with MX, SMTP, and disposable domain checks
- [Disposable Email Checker](https://apify.com/junipr/disposable-email-checker) — Check if emails are from disposable/temporary providers
- [Domain WHOIS Lookup](https://apify.com/junipr/domain-whois-lookup) — Get WHOIS and DNS data for any domain
- [Yellow Pages Scraper](https://apify.com/junipr/yellow-pages-scraper) — Scrape business listings with contact details from Yellow Pages
- [Bluesky Scraper](https://apify.com/junipr/bluesky-scraper) — Scrape social media posts and profiles from Bluesky