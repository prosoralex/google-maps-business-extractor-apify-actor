# Google Maps Business Extractor — Apify Actor usage guide

[![Run for free on Apify](https://img.shields.io/badge/Apify-Run%20it%20free%20%E2%80%94%20%245%2Fmo%20credit-24C1E0)](https://console.apify.com/sign-up?fpr=aupara)

Scrape Google Maps by keyword or URL. Extract business name, address, phone, website, rating, review count, opening hours & GPS coordinates. Supports bulk queries, residential proxy and direct place URLs. Export to JSON, CSV or Excel.

> **This repository does not contain the Actor's source code.** The Actor
> itself is closed-source and runs on Apify's infrastructure — this repo is
> just documentation and example client code showing how to call it via the
> Apify API/SDK with your own Apify API token. Think of it as a "cookbook"
> repo, not the product itself.

**Run it on Apify →** [https://apify.com/leadsbrary/google-maps-business-extractor?fpr=aupara](https://apify.com/leadsbrary/google-maps-business-extractor?fpr=aupara)

## What it does

A Google Maps scraper that extracts structured local business data from search queries or direct Google Maps place URLs: it captures business identity and category, contact details (address, phone, website), location coordinates and Plus Code, ratings and total review counts plus optional recent review text, weekly opening hours (optional), image URLs (up to 10 per place), price level, textual description and operational status (e.g., permanently closed), along with place identifiers and the original Maps URL. The Actor performs browser-based automation against Google Maps (uses real-browser navigation and page interactions, with fallback selectors for SPA changes), supports language and country biasing, configurable per-query result limits, and optional deeper page interactions to fetch reviews and opening schedules. Outputs are structured for use in lead generation, local SEO, business…

## Pricing

Pay-per-event pricing — you only pay for what the Actor actually delivers:

- **Actor Start** — $0.00005 (one-time, per run). Charged when the Actor starts running. Number of events charged depends on Actor memory (one event per GB, minimum one event).
- **Business result** — $0.003–$0.0015 depending on your Apify usage tier. One business extracted from Google Maps: name, address, phone, website, rating, reviews, opening hours and GPS coordinates.

*(Apify may also charge a small amount for the platform compute the Actor
uses while running — see the [pricing tab](https://apify.com/leadsbrary/google-maps-business-extractor?fpr=aupara) on the Actor page
for exact current numbers.)*

## Quick start

You need an Apify account and API token (`console.apify.com` → Settings →
Integrations). Don't have one yet? See the signup section below — new
accounts get **$5 of free usage credit every month**.

### cURL

```bash
curl -X POST "https://api.apify.com/v2/acts/leadsbrary~google-maps-business-extractor/runs?token=YOUR_APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
  "searchStringsArray": [
    "pizza New York",
    "coffee shop London"
  ],
  "startUrls": [],
  "maxCrawledPlaces": 3,
  "language": "en",
  "includeOpeningHours": true,
  "includeReviews": false,
  "maxReviews": 5,
  "proxyConfiguration": {
    "useApifyProxy": true
  }
}'
```

### Python (`apify-client`)

```python
from apify_client import ApifyClient

client = ApifyClient("YOUR_APIFY_TOKEN")

run_input = {
  "searchStringsArray": [
    "pizza New York",
    "coffee shop London"
  ],
  "startUrls": [],
  "maxCrawledPlaces": 3,
  "language": "en",
  "includeOpeningHours": True,
  "includeReviews": False,
  "maxReviews": 5,
  "proxyConfiguration": {
    "useApifyProxy": True
  }
}

run = client.actor("leadsbrary/google-maps-business-extractor").call(run_input=run_input)

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

### JavaScript (`apify-client`)

```javascript
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: 'YOUR_APIFY_TOKEN' });

const runInput = {
  "searchStringsArray": [
    "pizza New York",
    "coffee shop London"
  ],
  "startUrls": [],
  "maxCrawledPlaces": 3,
  "language": "en",
  "includeOpeningHours": true,
  "includeReviews": false,
  "maxReviews": 5,
  "proxyConfiguration": {
    "useApifyProxy": true
  }
};

const run = await client.actor('leadsbrary/google-maps-business-extractor').call(runInput);
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```

See [`example.py`](./example.py) in this repo for a complete runnable script.

## Don't have an Apify account yet?

[Sign up here](https://console.apify.com/sign-up?fpr=aupara) — new accounts get **$5 of free platform credit
every month**, enough to try most Actors without paying anything upfront.
Browsing for other tools? The full [Apify Store](https://apify.com/store?fpr=aupara) has thousands
of ready-made Actors.

## Links

- Actor page (run it, see live pricing/reviews): [https://apify.com/leadsbrary/google-maps-business-extractor?fpr=aupara](https://apify.com/leadsbrary/google-maps-business-extractor?fpr=aupara)
- All Actors from this developer: [https://apify.com/leadsbrary?fpr=aupara](https://apify.com/leadsbrary?fpr=aupara)
- Apify API docs: [https://docs.apify.com/api/v2](https://docs.apify.com/api/v2)

## License

The example code in this repository (README snippets, `example.py`) is
released under the MIT License — see [LICENSE](./LICENSE). This does not
cover the Actor itself, which remains closed-source and is operated by its
developer on the Apify platform.
