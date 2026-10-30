<p align="center">
  <a href="https://www.piloterr.com"><img src="images/banner.png" alt="Shophouzz Scraper API by Piloterr – scrape Shophouzz data as JSON" width="100%"></a>
</p>

# Shophouzz Scraper API

[![Discord](https://img.shields.io/badge/Discord-Join%20the%20community-5865F2?logo=discord&logoColor=white)](https://discord.gg/CFj3ph8aHU) [![Get API key](https://img.shields.io/badge/Piloterr-Get%20a%20free%20API%20key-111827)](https://app.piloterr.com) [![API docs](https://img.shields.io/badge/Docs-OpenAPI-0EA5E9)](https://app.piloterr.com/openapi) [![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

The **Piloterr Shophouzz Scraper API** lets you extract public data from Shophouzz as **clean, structured JSON** — no proxies, headless browsers or HTML parsing to maintain. Endpoints available in production:

- **Shophouzz Product API** — Retrieve full product details from Shophouzz, including title, price, variants, images, vendor, and structured metadata.

Use it for price monitoring, assortment tracking, competitor analysis, product research or catalog enrichment.

| Endpoint | Path | Credits | What you get |
|---|---|---|---|
| [Shophouzz Product API](#shophouzz-product-api) | `/v2/shophouzz/product` | 1 | Retrieve full product details from Shophouzz, including title, price, variants, images, vendor, and structured metadata. |

## Table of contents

- [How it works](#how-it-works)
- [Shophouzz Product API](#shophouzz-product-api)
- [Code examples in other languages](#code-examples-in-other-languages)
- [Practical use cases](#practical-use-cases)
- [Why Piloterr?](#why-piloterr)
- [FAQ](#faq)
- [Related scrapers](#related-scrapers)
- [Support](#support)

## How it works

1. **Create a free Piloterr account** and copy your API key from the [dashboard](https://app.piloterr.com).
2. **Send a `GET` (or `POST`) request** to `https://api.piloterr.com/v2/...` with the header `x-api-key: YOUR_API_KEY`.
3. **Receive structured JSON** — Piloterr handles rendering, proxies, retries and parsing.

```bash
export PILOTERR_API_KEY="your-api-key"
pip install requests        # Python
# TypeScript: Node.js 18+ (native fetch), run with `npx tsx file.ts`
```

> Every endpoint accepts both `GET` (query string) and `POST` (JSON body with the same fields).

## Shophouzz Product API

Retrieve full product details from Shophouzz, including title, price, variants, images, vendor, and structured metadata.

`GET | POST https://api.piloterr.com/v2/shophouzz/product` · **1 credit per request** · [Full reference](https://app.piloterr.com/openapi)

### Request parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `query` | string | ✅ | Full URL of the Shophouzz product page to retrieve details for. |

### Python example

```python
import json
import os
import requests

response = requests.get(
    "https://api.piloterr.com/v2/shophouzz/product",
    headers={"x-api-key": os.environ["PILOTERR_API_KEY"]},
    params={
        "query": "https://shophouzz.com/products/burke-counter-stool-cognac-vegan-leather-white-oak-veneer-metal-dowel-prvw-vr-186041078",
    },
    timeout=60,
)
response.raise_for_status()
data = response.json()

print(json.dumps(data, indent=2, ensure_ascii=False)[:2000])
```

### TypeScript example

```typescript
type ShophouzzProduct = {
  id?: number;
  tags?: string;
  image?: {
    id?: number;
    alt?: unknown;
    src?: string;
    width?: number;
    height?: number;
    position?: number;
    created_at?: string;
    product_id?: number;
    updated_at?: string;
    variant_ids?: unknown[];
  };
  title?: string;
  handle?: string;
  images?: {
    id?: number;
    alt?: unknown;
    src?: string;
    width?: number;
    height?: number;
    position?: number;
    created_at?: string;
    product_id?: number;
    updated_at?: string;
    variant_ids?: unknown[];
  }[];
  vendor?: string;
  options?: {
    id?: number;
    name?: string;
    values?: string[];
    position?: number;
    product_id?: number;
  }[];
  variants?: {
    id?: number;
    sku?: string;
    grams?: number;
    price?: string;
    title?: string;
    weight?: number;
    barcode?: string;
    option1?: string;
    option2?: string;
    option3?: string;
    taxable?: boolean;
    image_id?: unknown;
    position?: number;
    created_at?: string;
    product_id?: number;
    updated_at?: string;
    weight_unit?: string;
    quantity_rule?: {
      max?: unknown;
      min?: number;
      increment?: number;
    };
    price_currency?: string;
    compare_at_price?: string;
    requires_shipping?: boolean;
    fulfillment_service?: string;
    inventory_management?: string;
    quantity_price_breaks?: unknown[];
    compare_at_price_currency?: string;
  }[];
  body_html?: string;
  created_at?: string;
  updated_at?: string;
  product_type?: string;
  published_at?: string;
  published_scope?: string;
  template_suffix?: unknown;
};

const params = new URLSearchParams({
  "query": "https://shophouzz.com/products/burke-counter-stool-cognac-vegan-leather-white-oak-veneer-metal-dowel-prvw-vr-186041078",
});

const response = await fetch(`https://api.piloterr.com/v2/shophouzz/product?${params}`, {
  headers: { "x-api-key": process.env.PILOTERR_API_KEY! },
});
if (!response.ok) throw new Error(`Piloterr error ${response.status}: ${await response.text()}`);

const data = (await response.json()) as ShophouzzProduct;

console.log(JSON.stringify(data, null, 2).slice(0, 2000));
```

<details>
<summary><b>POST variant</b></summary>

```http
POST https://api.piloterr.com/v2/shophouzz/product
x-api-key: YOUR_API_KEY
Content-Type: application/json

{"query": "https://shophouzz.com/products/burke-counter-stool-cognac-vegan-leather-white-oak-veneer-metal-dowel-prvw-vr-186041078"}
```
</details>

### Output example

Example response from the API reference, abridged — real values depend on the page you scrape.

```json
{
  "id": 9992209793336,
  "tags": "assembly_required, best-seller, black, black faux leather, black faux leather straps, comfortable, compliance:cal-prop-65, contemporary, …",
  "image": {
    "id": 51424882983224,
    "alt": null,
    "src": "https://cdn.shopify.com/s/files/1/0941/8535/7624/files/d428cade-7856-43a2-b0ab-ad6d1fa4c68d.jpg?v=1770873702",
    "width": 478,
    "height": 990,
    "position": 1,
    "created_at": "2025-06-27T23:07:28-07:00",
    "product_id": 9992209793336,
    "updated_at": "2026-02-11T21:21:42-08:00",
    "variant_ids": []
  },
  "title": "Burke Counter Stool, Cognac, Vegan Leather, White Oak Veneer Metal Dowel",
  "handle": "burke-counter-stool-cognac-vegan-leather-white-oak-veneer-metal-dowel-prvw-vr-186041078",
  "images": [
    {
      "id": 51424882983224,
      "alt": null,
      "src": "https://cdn.shopify.com/s/files/1/0941/8535/7624/files/d428cade-7856-43a2-b0ab-ad6d1fa4c68d.jpg?v=1770873702",
      "width": 478,
      "height": 990,
      "position": 1,
      "created_at": "2025-06-27T23:07:28-07:00",
      "product_id": 9992209793336,
      "updated_at": "2026-02-11T21:21:42-08:00",
      "variant_ids": []
    },
    {
      "id": 51424882852152,
      "alt": null,
      "src": "https://cdn.shopify.com/s/files/1/0941/8535/7624/files/9f98d8da-988d-4d34-b3ff-90ddc25486cf.jpg?v=1770873702",
      "width": 990,
      "height": 990,
      "position": 2,
      "created_at": "2025-06-27T23:07:28-07:00",
      "product_id": 9992209793336,
      "updated_at": "2026-02-11T21:21:42-08:00",
      "variant_ids": []
    }
  ],
  "vendor": "Meridian Furniture",
  "options": [
    {
      "id": 12575493423416,
      "name": "Color",
      "values": [
        "Cognac"
      ],
      "position": 1,
      "product_id": 9992209793336
    },
    {
      "id": 12575493456184,
      "name": "Configuration",
      "values": [
        "White Oak Veneer Metal Dowel"
      ],
      "position": 2,
      "product_id": 9992209793336
    }
  ],
  "variants": [
    {
      "id": 50554338476344,
      "sku": "857Cognac-C",
      "grams": 14061,
      "price": "237.99",
      "title": "Cognac / White Oak Veneer Metal Dowel / Vegan Leather",
      "weight": 31,
      "barcode": "94308268583",
      "option1": "Cognac",
      "option2": "White Oak Veneer Metal Dowel",
      "option3": "Vegan Leather",
      "taxable": true,
      "image_id": null,
      "position": 1,
      "created_at": "2025-06-27T23:07:26-07:00",
      "product_id": 9992209793336,
      "updated_at": "2026-04-27T08:03:33-07:00",
      "weight_unit": "lb",
      "quantity_rule": {
        "max": null,
        "min": 1,
        "increment": 1
      },
      "price_currency": "USD",
      "compare_at_price": "",
      "requires_shipping": true,
      "fulfillment_service": "manual",
      "inventory_management": "shopify",
      "quantity_price_breaks": [],
      "compare_at_price_currency": ""
    }
  ],
  "body_html": "<p>Kick back and relax with a drink in your hand with this Burke cognac vegan leather counter stool. Featuring soft cognac vegan leather …",
  "created_at": "2025-06-27T23:07:26-07:00",
  "updated_at": "2026-04-27T08:03:33-07:00",
  "product_type": "Product",
  "published_at": "2025-06-27T23:07:27-07:00",
  "published_scope": "web",
  "template_suffix": null
}
```

### Response fields

| Field | Type | Description |
|---|---|---|
| `id` | integer |  |
| `tags` | string |  |
| `image` | object |  |
| `image.id` | integer |  |
| `image.alt` | object |  |
| `image.src` | string |  |
| `image.width` | integer |  |
| `image.height` | integer |  |
| `image.position` | integer |  |
| `image.created_at` | string |  |
| `image.product_id` | integer |  |
| `image.updated_at` | string |  |
| `image.variant_ids` | any[] |  |
| `title` | string |  |
| `handle` | string |  |
| `images[]` | object[] |  |
| `images[].id` | integer |  |
| `images[].alt` | object |  |
| `images[].src` | string |  |
| `images[].width` | integer |  |
| `images[].height` | integer |  |
| `images[].position` | integer |  |
| `images[].created_at` | string |  |
| `images[].product_id` | integer |  |
| `images[].updated_at` | string |  |

## Code examples in other languages

Ready-to-run examples live in the [`examples/`](examples) folder. Each one reads your key from the `PILOTERR_API_KEY` environment variable.

| Language | Product |
|---|---|
| cURL (Bash) | [`product`](examples/curl/product.sh) |
| PHP | [`product`](examples/php/product.php) |
| C# | [`product`](examples/csharp/Product.cs) |
| Go | [`product`](examples/go/product.go) |
| Java | [`product`](examples/java/ProductExample.java) |
| Ruby | [`product`](examples/ruby/product.rb) |
| Node.js | [`product`](examples/nodejs/product.mjs) |

## Practical use cases

- **Price monitoring** — Track prices, promotions and availability over time to react to competitors.
- **Assortment & catalog tracking** — Follow new products, delisted items and category changes.
- **Competitor analysis** — Benchmark ranges, brands and positioning across retailers.
- **Product research** — Spot best-sellers and trends from search results.
- **Catalog enrichment** — Pull titles, images and attributes into your PIM or marketplace listings.

## Why Piloterr?

- **No infrastructure** — no proxies, headless browsers or CAPTCHA solving to run yourself.
- **Structured JSON** — stable, documented fields instead of brittle HTML selectors.
- **Pay per request** — transparent credit cost per endpoint, failed requests are retried for you.
- **One API key, hundreds of sources** — Shophouzz plus many other e-commerce, search and company data endpoints in the [Piloterr library](https://www.piloterr.com/library).
- **Any language** — plain HTTPS + JSON, with examples for Python, TypeScript, cURL, PHP, C#, Go, Java, Ruby and Node.js.

## FAQ

### Is it legal to scrape Shophouzz?

Collecting publicly available data is generally allowed in many jurisdictions, but rules depend on your country, the data you collect and how you use it. Avoid personal data unless you have a lawful basis, respect the website's terms where they apply, and get legal advice for your specific use case. This is not legal advice.

### Do I need proxies or a headless browser?

No. Piloterr handles rendering, proxy rotation and retries on its side. You only send an HTTPS request with your `x-api-key` header and receive JSON.

### How much does a request cost?

Credits per call: `/v2/shophouzz/product` **1**. See the [Piloterr website](https://www.piloterr.com) for plans.

### What data does the Shophouzz API return?

Each endpoint returns structured JSON: **Shophouzz Product** — `id`, `tags`, `image`, `image.id`, `image.alt`, `image.src`.

### Which languages are supported?

Any language that can make an HTTP request. This README shows Python and TypeScript; the [`examples/`](examples) folder contains cURL, PHP, C#, Go, Java, Ruby and Node.js.

## Related scrapers

- [About You Scraper API](https://github.com/piloterr/aboutyou-scraper)
- [Action Scraper API](https://github.com/piloterr/action-scraper)
- [Aldi Scraper API](https://github.com/piloterr/aldi-scraper)
- [Alibaba Scraper API](https://github.com/piloterr/alibaba-scraper)
- [AliExpress Scraper API](https://github.com/piloterr/aliexpress-scraper)
- [Allegro Scraper API](https://github.com/piloterr/allegro-scraper)
- [All Piloterr scrapers on GitHub](https://github.com/piloterr)

## Support

- 💬 Join the [Piloterr Discord](https://discord.gg/CFj3ph8aHU) to ask questions and share what you build.
- 📚 Browse the [API reference (OpenAPI)](https://app.piloterr.com/openapi) and the [Piloterr library](https://www.piloterr.com/library).
- 🔑 [Get your API key](https://app.piloterr.com).

---

<p align="center">
  <a href="https://www.piloterr.com">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="images/logo-dark.svg">
      <img src="images/logo.svg" alt="Piloterr" height="32">
    </picture>
  </a>
  <br>
  <sub>Built by <a href="https://www.piloterr.com">Piloterr</a> — web scraping APIs for e-commerce, search, real estate and more, one API key.</sub>
</p>

<sub>Shophouzz is a trademark of its respective owner. This repository is not affiliated with or endorsed by Shophouzz. Examples are released under the MIT license.</sub>
