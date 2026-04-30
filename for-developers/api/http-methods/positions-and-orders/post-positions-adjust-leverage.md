---
description: Adjust isolated leverage.
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/ding-dan-yu-cang-wei/diao-zheng-gang-gan-post-positionsadjustleverage
---

# POST positions/adjust-leverage

```
POST /v1/private/exchange/positions/adjust-leverage
```

#### Request Body

| Field              | Type   | Required | Description                                                                                                                   |
| ------------------ | ------ | -------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `client_adjust_id` | string | Yes      | ClientAdjustID is required and must be a UUID.                                                                                |
| `position_uid`     | string | Yes      | PositionUID is required to indicate the specific position by position to be adjusted.                                         |
| `target_leverage`  | string | Yes      | TargetLeverage must be a positive integer string and the actual effective value cannot exceed the upper limit of the runtime. |

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
