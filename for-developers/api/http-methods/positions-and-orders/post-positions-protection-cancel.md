---
description: Cancel TP/SL protection on a position.
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/ding-dan-yu-cang-wei/qu-xiao-cang-wei-bao-hu-post-positionsprotectioncancel
---

# POST positions/protection/cancel

```
POST /v1/private/exchange/positions/protection/cancel
```

#### Request Body

| Field          | Type   | Required | Description                                                                                                           |
| -------------- | ------ | -------- | --------------------------------------------------------------------------------------------------------------------- |
| `position_uid` | string | Yes      | PositionUID is required, indicating that the specific position by position of the protection rule is to be cancelled. |
| `target`       | string | Yes      | Target is required and can be take\_profit, stop\_loss, or both.                                                      |

#### Response

```json
{
  "success": true,
  "data": {
    "position": {}
  }
}
```

#### Response Fields

| Field                                | Type    | Description |
| ------------------------------------ | ------- | ----------- |
| `data`                               | object  |             |
| `data.position`                      | object  |             |
| `data.position.avg_close_price`      | string  |             |
| `data.position.closed_quantity`      | string  |             |
| `data.position.entry_price`          | string  |             |
| `data.position.leverage`             | string  |             |
| `data.position.liquidation_price`    | string  |             |
| `data.position.margin`               | string  |             |
| `data.position.opened_at`            | string  |             |
| `data.position.positionUid`          | string  |             |
| `data.position.realized_pnl`         | string  |             |
| `data.position.side`                 | string  |             |
| `data.position.size`                 | string  |             |
| `data.position.stop_loss_price`      | string  |             |
| `data.position.stop_loss_quantity`   | string  |             |
| `data.position.symbol`               | string  |             |
| `data.position.take_profit_price`    | string  |             |
| `data.position.take_profit_quantity` | string  |             |
| `success`                            | boolean |             |
