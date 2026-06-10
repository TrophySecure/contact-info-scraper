[Contact Info Scraper](https://apify.com/lanky_quantifier/contact-info-scraper?fpr=data)

# Contact Info Scraper

Extract emails, phone numbers, and social media profiles from any website automatically. Perfect for lead generation, business intelligence, and contact database building.

## What is Contact Info Scraper?

Contact Info Scraper is a powerful web scraping tool that automatically extracts contact information from websites, including email addresses, phone numbers, and social media links. Unlike manual data collection, this actor crawls multiple pages on each domain, intelligently follows contact and about pages, and aggregates all discovered contact details into a structured dataset.

The scraper uses advanced pattern recognition to identify contact information across different formats and languages. It validates email addresses, normalizes phone numbers to international formats, and detects social media profiles across 7 major platforms including Facebook, Instagram, Twitter/X, LinkedIn, YouTube, TikTok, and GitHub.

Whether you're building a prospecting list, enriching your CRM database, or conducting market research, Contact Info Scraper saves hours of manual work by automatically gathering contact details from hundreds of websites in minutes. The built-in deduplication and false positive filtering ensures you receive clean, actionable data ready for immediate use.

## What data does it extract?

| Field | Type | Description |
| --- | --- | --- |
| `inputUrl` | string | The original URL you provided for scraping |
| `domain` | string | The website's domain name (e.g., example.com) |
| `emails` | array | All unique email addresses found across all crawled pages |
| `primaryEmail` | string | The first email address found (typically the main contact) |
| `phones` | array | All unique phone numbers found, normalized to international format |
| `primaryPhone` | string | The first phone number found (typically the main contact) |
| `socialLinks` | object | Object containing all discovered social media profile URLs |
| `facebook` | string | Facebook page or profile URL |
| `instagram` | string | Instagram profile URL |
| `twitter` | string | Twitter/X profile URL |
| `linkedin` | string | LinkedIn company or personal profile URL |
| `youtube` | string | YouTube channel URL |
| `tiktok` | string | TikTok profile URL |
| `github` | string | GitHub organization or user profile URL |
| `emailCount` | number | Total number of unique emails found |
| `phoneCount` | number | Total number of unique phones found |
| `socialCount` | number | Total number of social media profiles found |
| `scrapedAt` | string | ISO 8601 timestamp of when the data was scraped |

## How to scrape contact information from websites

1. **Prepare your URL list**: Create a list of website URLs you want to scrape. You can include URLs with or without `http://` or `https://` - the scraper automatically adds the protocol if missing.
2. **Configure crawling depth**: Set `maxPagesPerDomain` to control how many pages per website to crawl. Use 5 for quick scans, 10-15 for standard scraping, or 20-50 for comprehensive extraction from large websites.
3. **Enable smart page following**: Keep `followContactPages` enabled (default: true) to automatically detect and crawl Contact, About, Imprint, Team, and similar pages where contact information is typically found.
4. **Start the actor**: Run the actor from the Apify Console or via API. The scraper will crawl each website concurrently, extracting all available contact information.
5. **Download results**: Once completed, export your data in JSON, CSV, Excel, or XML format. Each website will have one aggregated record with all contact details found across multiple pages.
6. **Filter and process**: Use the structured output fields to filter results (e.g., only websites with emails, only those with social profiles) and integrate with your CRM, marketing automation, or spreadsheet tools.
7. **Automate workflows**: Set up scheduled runs to regularly update contact databases or integrate with Zapier, Make, or webhooks to trigger actions when new contact information is discovered.

## Input parameters

| Parameter | Type | Required | Description | Default |
| --- | --- | --- | --- | --- |
| `urls` | array | Yes | List of website URLs to extract contact information from. Accepts URLs with or without protocol (http/https). | - |
| `maxPagesPerDomain` | integer | No | Maximum number of pages to crawl per website. Higher values increase coverage but take longer. Range: 1-50. | 5 |
| `followContactPages` | boolean | No | Automatically detect and follow links to Contact, About, Imprint, Team, and similar pages where contact info is typically located. | true |

## Example input

```
{
  "urls": [
    "https://example-startup.com",
    "techcompany.io",
    "www.business-consulting.de",
    "marketingagency.co.uk"
  ],
  "maxPagesPerDomain": 10,
  "followContactPages": true
}
```

## Example output

```
{
  "inputUrl": "https://example-startup.com",
  "domain": "example-startup.com",
  "emails": [
    "hello@example-startup.com",
    "sales@example-startup.com",
    "support@example-startup.com",
    "jobs@example-startup.com"
  ],
  "primaryEmail": "hello@example-startup.com",
  "phones": [
    "+1 (415) 555-0123",
    "+44 20 7946 0958"
  ],
  "primaryPhone": "+1 (415) 555-0123",
  "socialLinks": {
    "facebook": "https://facebook.com/examplestartup",
    "instagram": "https://instagram.com/examplestartup",
    "twitter": "https://x.com/examplestartup",
    "linkedin": "https://linkedin.com/company/example-startup",
    "youtube": "https://youtube.com/c/examplestartup",
    "github": "https://github.com/example-startup"
  },
  "facebook": "https://facebook.com/examplestartup",
  "instagram": "https://instagram.com/examplestartup",
  "twitter": "https://x.com/examplestartup",
  "linkedin": "https://linkedin.com/company/example-startup",
  "youtube": "https://youtube.com/c/examplestartup",
  "github": "https://github.com/example-startup",
  "emailCount": 4,
  "phoneCount": 2,
  "socialCount": 6,
  "scrapedAt": "2024-02-15T14:30:00.000Z"
}
```

## Is it legal to scrape contact information?

Web scraping publicly available contact information is generally legal when the data is accessible without authentication and intended for public viewing. Contact details displayed on business websites, such as general inquiry emails, public phone numbers, and links to social media profiles, are typically published with the intent of being found and used for legitimate business communication.

However, you should always comply with applicable laws and regulations in your jurisdiction, including GDPR in Europe, CCPA in California, and similar data protection laws. Use scraped contact information responsibly and ethically - only for legitimate business purposes such as B2B outreach, market research, or directory building. Do not use this tool to harvest personal data for spam, harassment, or any activity that violates privacy laws or platform terms of service. Always provide opt-out mechanisms and respect data subject rights when using contact information for marketing purposes.

## Pricing

This actor is free to use. You only pay for Apify platform usage based on compute units consumed during scraping. Typical cost is $0.01-0.05 per 100 websites scraped, depending on crawling depth and page complexity.

## FAQ

**How many websites can I scrape at once?**
There is no hard limit on the number of URLs you can process in a single run. The actor processes websites concurrently for optimal performance. For large batches (1000+ websites), consider splitting into multiple runs or increasing memory allocation to 8192 MB for better performance. A typical run of 100 websites with default settings completes in 5-15 minutes.

**Does it find emails behind contact forms?**
No, the scraper extracts only publicly visible contact information from page content, mailto links, and tel links. It cannot extract emails that are hidden behind contact forms, JavaScript obfuscation, or CAPTCHA-protected pages. However, it intelligently crawls contact pages where emails are often displayed alongside forms, maximizing the chances of finding direct contact addresses.

**What formats are supported for export?**
Results can be exported in JSON, JSON Lines, CSV, Excel (XLSX), XML, RSS, and HTML table formats. JSON is recommended for API integrations and further processing. CSV and Excel are ideal for importing into spreadsheets and CRM systems. All formats preserve the complete data structure including arrays of emails, phones, and social links.

**How accurate is the email extraction?**
The scraper achieves high accuracy through multi-layered validation: it extracts emails from both mailto links and page text, validates format using regex patterns, and filters common false positives like [example@domain.com](mailto:example@domain.com), [test@test.com](mailto:test@test.com), and emails from third-party services (Google APIs, WordPress.org, etc.). Typical accuracy is 95%+ for real business emails, with occasional false positives from legal disclaimers or embedded third-party widgets.

**Can I scrape websites in languages other than English?**
Yes, the scraper works with websites in any language. Phone number normalization supports international formats, and the contact page detection includes multilingual keywords (Contact, Kontakt, Imprint, Impressum, etc.). Email and social media link extraction are language-agnostic as they rely on URL patterns and format validation rather than text analysis.

## Related actors

- **Google Maps Scraper** - Extract business contact information, phone numbers, and websites from Google Maps local search results
- **LinkedIn Company Scraper** - Gather company contact details, employee counts, and social links from LinkedIn profiles
- **Yellow Pages Scraper** - Extract business listings with phone numbers, addresses, and categories from online directories
- **Email Verification Tool** - Validate and verify email addresses extracted from websites to improve deliverability and reduce bounces

## Proxy Recommendations

For best results, use residential or datacenter proxies:

- 🔗 **[Smartproxy](https://smartproxy.com/?via=apify)** — Residential proxies with 195+ locations. **50% revenue share** for referrals. Best for social media and SERP scraping.
- 🔗 **[Bright Data](https://brightdata.com/?via=vss)** — Enterprise-grade proxies used by Fortune 500. Up to 25% commission. Best for large-scale extraction.

> 💡 These actors work out-of-the-box with Apify's built-in proxy pool too.

## 🛒 Get More Tools

Looking for ready-made automation kits?

- 📦 **[Apify Scrapers Bundle ($29)](https://vhubster3.gumroad.com/l/apify-bundle)** — 10+ actors in one package
- ⚡ **[n8n Automation Pack ($39)](https://vhubster3.gumroad.com/l/n8n-pack)** — Pre-built workflows for scraping pipelines