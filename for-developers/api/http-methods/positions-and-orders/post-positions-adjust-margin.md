---
description: Add or remove isolated margin.
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/ding-dan-yu-cang-wei/diao-zheng-bao-zheng-jin-post-positionsadjustmargin
---

# POST positions/adjust-margin

```
POST /v1/private/exchange/positions/adjust-margin
```

#### Request Body

| Field              | Type   | Required | Description                                                                                                                        |
| ------------------ | ------ | -------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `client_adjust_id` | string | Yes      | ClientAdjustID is required and must be a UUID.                                                                                     |
| `delta_margin`     | string | Yes      | DeltaMargin must be a non-zero decimal string; positive numbers represent margin calls and negative numbers represent margin cuts. |
| `position_uid`     | string | Yes      | PositionUID is required to indicate the specific position by position to be adjusted.                                              |

#### Response

```json
{
  "success": true,
  "data": {
    "ledger_tx_id": "...",
    "leverage": "...",
    "liquidation_price": "...",
    "margin": "...",
    "position_uid": "..."
  }
}
```

#### Response Fields

| Field                    | Type    | Description                                                                                      |
| ------------------------ | ------- | ------------------------------------------------------------------------------------------------ |
| `data`                   | object  |                                                                                                  |
| `data.ledger_tx_id`      | string  |                                                                                                  |
| `data.leverage`          | string  |                                                                                                  |
| `data.liquidation_price` | string  | LiquidationPrice returns an estimated strong parity for the persistence of the current position. |
| `data.margin`            | string  |                                                                                                  |
| `data.position_uid`      | string  |                                                                                                  |
| `success`                | boolean |                                                                                                  |
