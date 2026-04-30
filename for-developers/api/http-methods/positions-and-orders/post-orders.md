---
description: Create order.
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/ding-dan-yu-cang-wei/chuang-jian-ding-dan-post-orders
---

# POST orders

```
POST /v1/private/exchange/orders
```

#### Request Body

| Field                    | Type       | Required | Description                                                                                                                                                                                                         |
| ------------------------ | ---------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `cost`                   | string     | No       | Choose between Cost and Quantity; total cost budget (including margin and handling fee), the semantics are the same as post/orders/by-cost.                                                                         |
| `insurances`             | object \[] | No       | Insurances optional; only available if order\_type = market. The incoming "open and insure" link will be taken, and a single request can contain multiple insurance items.                                          |
| `acceptUnlimitedPremium` | boolean    | No       |                                                                                                                                                                                                                     |
| `durationHours`          | integer    | Yes      |                                                                                                                                                                                                                     |
| `insuranceType`          | string     | Yes      |                                                                                                                                                                                                                     |
| `payoutPercent`          | integer    | No       |                                                                                                                                                                                                                     |
| `premiumLimit`           | string     | No       |                                                                                                                                                                                                                     |
| `triggerPercent`         | integer    | No       |                                                                                                                                                                                                                     |
| `leverage`               | string     | No       | Leverage is optional and must be an integer string greater than 0 and not greater than 100; condition sheets do not apply.                                                                                          |
| `limit_price`            | string     | No       | LimitPrice is required when order\_type = limit; market and position protection setup scenarios must be omitted.                                                                                                    |
| `order_type`             | string     | Yes      | OrderType only accepts market, limit, stop\_loss, take\_profit; where stop\_loss/take\_profit means directly setting position protection rules.                                                                     |
| `position_uid`           | string     | No       | PositionUID is required when stop\_loss/take\_profit standalone position protection is set to precisely bind the target position; market/limit master order is usually omitted.                                     |
| `quantity`               | string     | No       | Choose between Quantity and Cost (market/limit main order and insurance); `quantity` is a positive number string; independent stop\_loss/take\_profit only supports quantity.                                       |
| `side`                   | string     | No       | Side is required in the market/limit main single scenario (only buy or sell is accepted); independent stop\_loss/take\_profit scenarios will automatically derive and ignore this field according to position\_uid. |
| `stop_loss_price`        | string     | No       | StopLossPrice is required when order\_type = stop\_loss; in the market/limit main order, it indicates the stop loss trigger price to be attached after closing the position.                                        |
| `stop_loss_quantity`     | string     | No       | StopLossQuantity is only valid for market/limit main orders; when omitted, it is equal to the main order quantity by default.                                                                                       |
| `symbol`                 | string     | No       | Symbol is the symbol of the transaction pair (such as BTC-USD); market/limit master order is required, and the independent stop\_loss/take\_profit scenario can be omitted (parsed by position\_uid).               |
| `take_profit_price`      | string     | No       | TakeProfitPrice is required when order\_type = take\_profit; in the market/limit main order, indicate the take profit trigger price to be attached after closing the position.                                      |
| `take_profit_quantity`   | string     | No       | TakeProfitQuantity is only valid for market/limit main orders; when omitted, it is equal to the main order quantity by default.                                                                                     |

#### Response

```json
{
  "success": true,
  "data": {
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
| `data.side`                              | string     |             |
| `data.status`                            | string     |             |
| `data.symbol`                            | string     |             |
| `success`                                | boolean    |             |
