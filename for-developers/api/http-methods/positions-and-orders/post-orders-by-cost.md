---
description: Create order by total cost budget.
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/ding-dan-yu-cang-wei/an-cheng-ben-yu-suan-xia-dan-post-ordersbycost
---

# POST orders/by-cost

```
POST /v1/private/exchange/orders/by-cost
```

#### Request Body

| Field                  | Type   | Required | Description                                                                                                                                                                                       |
| ---------------------- | ------ | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `cost`                 | string | Yes      | Cost is the total cost (including security deposits and fees) acceptable to the user.                                                                                                             |
| `leverage`             | string | No       | Leverage is optional and must be an integer string greater than 0 and not greater than 100; condition sheets do not apply.                                                                        |
| `limit_price`          | string | No       | LimitPrice is required when order\_type = limit; other scenarios must be omitted.                                                                                                                 |
| `order_type`           | string | Yes      | OrderType only accepts market, limit; stop\_loss/take\_profit position protection settings are not supported for cost orders.                                                                     |
| `position_uid`         | string | No       | PositionUID is reserved for additional protection rules that need to be routed by position; currently only market/limit master orders are supported for orders at cost, which is usually omitted. |
| `side`                 | string | Yes      | Side only accepts buy or sell.                                                                                                                                                                    |
| `stop_loss_price`      | string | No       | StopLossPrice is optional; it is only valid for market/limit main orders, indicating the stop loss trigger price to be attached after the main order is closed.                                   |
| `stop_loss_quantity`   | string | No       | StopLossQuantity is optional; omitted by default is equal to the number of Master Orders that the system reverse-costs.                                                                           |
| `symbol`               | string | Yes      | Symbols are trading pair symbols, such as BTC-USD.                                                                                                                                                |
| `take_profit_price`    | string | No       | TakeProfitPrice is optional; it is only valid for market/limit main orders, indicating the take profit trigger price that will accompany the closing of the main order.                           |
| `take_profit_quantity` | string | No       | TakeProfitQuantity is optional; omitted by default is equal to the number of Master Orders that the system reverse-costs.                                                                         |

#### Response

```json
{
  "success": true,
  "data": {
    "computed_fee": "...",
    "computed_margin": "...",
    "computed_quantity": "...",
    "executed": true,
    "execution_slippage_bps": "...",
    "fee": "...",
    "fill_id": "...",
    "filled_quantity": "...",
    "insurance_policies": [],
    "insurance_policy_ids": "...",
    "insurance_total_premium": "...",
    "ledger_tx_id": "...",
    "mark_price": "...",
    "order_filled_quantity": "...",
    "order_id": "...",
    "order_type": "...",
    "position_uid": "...",
    "price": "...",
    "protection_id": "...",
    "reference_price": "...",
    "side": "...",
    "status": "...",
    "symbol": "..."
  }
}
```

#### Response Fields

| Field                                    | Type       | Description |
| ---------------------------------------- | ---------- | ----------- |
| `data`                                   | object     |             |
| `data.computed_fee`                      | string     |             |
| `data.computed_margin`                   | string     |             |
| `data.computed_quantity`                 | string     |             |
| `data.executed`                          | boolean    |             |
| `data.execution_slippage_bps`            | string     |             |
| `data.fee`                               | string     |             |
| `data.fill_id`                           | string     |             |
| `data.filled_quantity`                   | string     |             |
| `data.insurance_policies`                | object \[] |             |
| `data.insurance_policies.expiresAt`      | integer    |             |
| `data.insurance_policies.insuranceType`  | string     |             |
| `data.insurance_policies.payoutAmount`   | string     |             |
| `data.insurance_policies.payoutPercent`  | integer    |             |
| `data.insurance_policies.policyId`       | string     |             |
| `data.insurance_policies.premium`        | string     |             |
| `data.insurance_policies.triggerPercent` | integer    |             |
| `data.insurance_policies.triggerPrice`   | string     |             |
| `data.insurance_policies.tx_hash`        | string     |             |
| `data.insurance_policy_ids`              | string \[] |             |
| `data.insurance_total_premium`           | string     |             |
| `data.ledger_tx_id`                      | string     |             |
| `data.mark_price`                        | string     |             |
| `data.order_filled_quantity`             | string     |             |
| `data.order_id`                          | string     |             |
| `data.order_type`                        | string     |             |
| `data.position_uid`                      | string     |             |
| `data.price`                             | string     |             |
| `data.protection_id`                     | string     |             |
| `data.reference_price`                   | string     |             |
| `data.side`                              | string     |             |
| `data.status`                            | string     |             |
| `data.symbol`                            | string     |             |
| `success`                                | boolean    |             |
