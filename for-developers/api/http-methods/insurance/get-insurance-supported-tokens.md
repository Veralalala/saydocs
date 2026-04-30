---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/bao-xian/huo-qu-zhi-chi-de-dai-bi-get-insurancesupportedtokens
---

# GET insurance/supported-tokens

Query currently insurable markets, supported insurance types, leverage windows, and duration windows (public endpoint).

```
GET /v1/public/insurance/supported-tokens
```

#### Response

```json
{
  "success": true,
  "minQuoteIsolatedMargin": "10",
  "data": [
    {
      "symbol": "BTC-USD",
      "market": "BTC-USD",
      "insuranceTypes": [
        { "code": "REVIVAL", "type": 1 }
      ],
      "minLeverage": "2",
      "maxLeverage": "50",
      "minDurationHours": 24,
      "maxDurationHours": 168
    }
  ]
}
```
