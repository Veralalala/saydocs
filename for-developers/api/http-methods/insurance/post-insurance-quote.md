---
description: Insurance quote (public).
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/bao-xian/qu-de-bao-xian-bao-jia-post-insurancequote
---

# POST insurance/quote

```
POST /v1/public/insurance/quote
```

#### Request Body

| Field              | Type    | Required | Description                                                                                                                                 |
| ------------------ | ------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `currentMarkPrice` | string  | No       |                                                                                                                                             |
| `durationHours`    | integer | No       |                                                                                                                                             |
| `position`         | object  | Yes      |                                                                                                                                             |
| `entryPrice`       | string  | Yes      |                                                                                                                                             |
| `insuranceType`    | string  | Yes      |                                                                                                                                             |
| `leverage`         | string  | Yes      |                                                                                                                                             |
| `liquidationPrice` | string  | No       | LiquidationPrice is optional. Zero Loss quotes usually pass a value aligned with `positions.liquidation_price` when pricing open positions. |
| `margin`           | string  | Yes      |                                                                                                                                             |
| `payoutPercent`    | integer | No       |                                                                                                                                             |
| `side`             | string  | Yes      |                                                                                                                                             |
| `symbol`           | string  | Yes      |                                                                                                                                             |
| `triggerPercent`   | integer | No       |                                                                                                                                             |

#### Response

```json
{
  "success": true,
  "data": {
    "quote": {},
    "quotes": []
  }
}
```

#### Response Fields

| Field                                     | Type       | Description |
| ----------------------------------------- | ---------- | ----------- |
| `data`                                    | object     |             |
| `data.quote`                              | object     |             |
| `data.quote.barrierPrice`                 | string     |             |
| `data.quote.durationHours`                | integer    |             |
| `data.quote.entryPrice`                   | string     |             |
| `data.quote.insuranceType`                | integer    |             |
| `data.quote.leverage`                     | string     |             |
| `data.quote.margin`                       | string     |             |
| `data.quote.markPriceSnapshot`            | string     |             |
| `data.quote.market`                       | string     |             |
| `data.quote.notional`                     | string     |             |
| `data.quote.payoutAmount`                 | string     |             |
| `data.quote.payoutPercent`                | integer    |             |
| `data.quote.positionSize`                 | string     |             |
| `data.quote.premiumPreview`               | object     |             |
| `data.quote.premiumPreview.totalPremium`  | string     |             |
| `data.quote.pricedAt`                     | integer    |             |
| `data.quote.side`                         | integer    |             |
| `data.quote.symbol`                       | string     |             |
| `data.quote.triggerPercent`               | integer    |             |
| `data.quotes`                             | object \[] |             |
| `data.quotes.barrierPrice`                | string     |             |
| `data.quotes.durationHours`               | integer    |             |
| `data.quotes.entryPrice`                  | string     |             |
| `data.quotes.insuranceType`               | integer    |             |
| `data.quotes.leverage`                    | string     |             |
| `data.quotes.margin`                      | string     |             |
| `data.quotes.markPriceSnapshot`           | string     |             |
| `data.quotes.market`                      | string     |             |
| `data.quotes.notional`                    | string     |             |
| `data.quotes.payoutAmount`                | string     |             |
| `data.quotes.payoutPercent`               | integer    |             |
| `data.quotes.positionSize`                | string     |             |
| `data.quotes.premiumPreview`              | object     |             |
| `data.quotes.premiumPreview.totalPremium` | string     |             |
| `data.quotes.pricedAt`                    | integer    |             |
| `data.quotes.side`                        | integer    |             |
| `data.quotes.symbol`                      | string     |             |
| `data.quotes.triggerPercent`              | integer    |             |
| `success`                                 | boolean    |             |
