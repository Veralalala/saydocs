---
description: Ledger txs linked to an order.
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/ding-dan-yu-cang-wei/qu-de-ding-dan-zhang-ben-liu-shui-get-privateexplorerordersidledgertxs
---

# GET private/explorer/orders/{id}/ledger-txs

```
GET /v1/private/explorer/orders/{id}/ledger-txs
```

#### Path Parameters

| Parameter | Required | Description     |
| --------- | -------- | --------------- |
| `id`      | Yes      | The order UUID. |

#### Response

```json
{
  "success": true,
  "data": {
    "order_id": "...",
    "transactions": []
  }
}
```

#### Response Fields

| Field                          | Type       | Description                                                                                     |
| ------------------------------ | ---------- | ----------------------------------------------------------------------------------------------- |
| `data`                         | object     |                                                                                                 |
| `data.order_id`                | string     |                                                                                                 |
| `data.transactions`            | object \[] |                                                                                                 |
| `data.transactions.created_at` | string     | Flow creation time, UTC.                                                                        |
| `data.transactions.kind`       | string     | Ledger flow type.                                                                               |
| `data.transactions.line_count` | integer    | The number of ledger lines included in the flow.                                                |
| `data.transactions.tx_hash`    | string     | Ledger flow hash. Natively derived from the real `tx_id`, does not return the original `tx_id`. |
| `success`                      | boolean    |                                                                                                 |
