---
description: Paginated rolling 24h tickers.
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/shi-chang/qu-de-24-xiao-shi-tickerget-publicexplorerticker
---

# GET public/explorer/ticker

```
GET /v1/public/marketdata/ticker
```

#### Query Parameters

| Parameter  | Required | Description                                                   |
| ---------- | -------- | ------------------------------------------------------------- |
| `sort`     | No       | volume\_\* Sorted by quote turnover q (same as rank ZSET)     |
| `category` | No       | `all` or DB column `instrument_type` (API side name category) |
| `limit`    | No       |                                                               |
| `cursor`   | No       | Last response 'next\_cursor\`                                 |

#### Response

```json
{
  "success": true,
  "data": {}
}
```

#### Response Fields

| Field              | Type       | Description                                                                                                                   |
| ------------------ | ---------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `category`         | string     | Consistent with request parameter `category`; corresponds to filtering DB `instrument_type`                                   |
| `count`            | integer    |                                                                                                                               |
| `items`            | object \[] |                                                                                                                               |
| `items.rank_score` | number     | The score of the current sort corresponding to the ZSET (percentage point increase or decrease; volume is the quote turnover) |
| `items.symbol`     | string     |                                                                                                                               |
| `items.ticker`     | object     | Redis 'oracle: ticker24h \`JSON; omitted if missing                                                                           |
| `limit`            | integer    |                                                                                                                               |
| `next_cursor`      | string     | Next page cursor; empty means no more data                                                                                    |
| `sort`             | string     |                                                                                                                               |
