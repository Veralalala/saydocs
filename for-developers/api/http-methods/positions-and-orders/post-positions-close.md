---
description: Close position (full or partial).
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/ding-dan-yu-cang-wei/ping-cang-post-positionsclose
---

# POST positions/close

```
POST /v1/private/exchange/positions/close
```

#### Request Body

| Field             | Type   | Required | Description                                                                                                                         |
| ----------------- | ------ | -------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| `client_close_id` | string | No       | ClientCloseID becomes required when a quantity is passed in and must be a UUID.                                                     |
| `position_uid`    | string | Yes      | PositionUID is required to indicate the specific position by position to be closed.                                                 |
| `quantity`        | string | No       | Quantity is optional; omitted means fully flat, passed value means partially closed position, and must be a positive number string. |

#### Response

```json
{
  "success": true,
  "data": {
    "close_avg_price": "...",
    "closed_quantity": "...",
    "fee": "...",
    "is_full_close": true,
    "ledger_tx_id": "...",
    "pnl": "...",
    "proceeds": "...",
    "remaining_margin": "...",
    "remaining_size": "..."
  }
}
```

#### Response Fields

| Field                   | Type    | Description |
| ----------------------- | ------- | ----------- |
| `data`                  | object  |             |
| `data.close_avg_price`  | string  |             |
| `data.closed_quantity`  | string  |             |
| `data.fee`              | string  |             |
| `data.is_full_close`    | boolean |             |
| `data.ledger_tx_id`     | string  |             |
| `data.pnl`              | string  |             |
| `data.proceeds`         | string  |             |
| `data.remaining_margin` | string  |             |
| `data.remaining_size`   | string  |             |
| `success`               | boolean |             |
