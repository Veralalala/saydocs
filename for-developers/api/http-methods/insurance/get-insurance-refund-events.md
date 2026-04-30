---
description: Refund events (public).
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/bao-xian/qu-de-tui-fei-shi-jian-get-insurancerefundevents
---

# GET insurance/refund-events

```
GET /v1/public/insurance/refund-events
```

#### Query Parameters

| Parameter | Required | Description                                                                  |
| --------- | -------- | ---------------------------------------------------------------------------- |
| `address` | No       | User EVM address (0x...); option with X-Sayfi-User-Address, header preferred |
| `limit`   | No       | Number of bars per page, default 20, maximum 200                             |
| `offset`  | No       | Offset, default 0                                                            |

#### Response

```json
{
  "success": true,
  "data": {
    "items": [],
    "limit": 0,
    "offset": 0,
    "total": 0
  }
}
```

#### Response Fields

| Field                            | Type       | Description |
| -------------------------------- | ---------- | ----------- |
| `data`                           | object     |             |
| `data.items`                     | object \[] |             |
| `data.items.createdAt`           | integer    |             |
| `data.items.currency`            | string     |             |
| `data.items.policyId`            | string     |             |
| `data.items.reason`              | string     |             |
| `data.items.refundAmount`        | string     |             |
| `data.items.refundEventId`       | string     |             |
| `data.items.replacementPolicyId` | string     |             |
| `data.items.resolvedAt`          | integer    |             |
| `data.items.tx_hash_refund`      | string     |             |
| `data.limit`                     | integer    |             |
| `data.offset`                    | integer    |             |
| `data.total`                     | integer    |             |
| `success`                        | boolean    |             |
