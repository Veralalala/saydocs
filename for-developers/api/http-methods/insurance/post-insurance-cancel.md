---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/bao-xian/tui-bao-post-insurancecancel
---

# POST insurance/cancel

Cancel an active insurance policy and initiate a refund.

```
POST /v1/private/insurance/cancel
```

#### Request Body

| Field                   | Type   | Required | Description                       |
| ----------------------- | ------ | -------- | --------------------------------- |
| `policyId`              | string | Yes      | ID of the active policy to cancel |
| `requestIdempotencyKey` | string | Yes      | Idempotency key                   |

> After cancellation, the policy status transitions through `refunding` → `cancelled`. The `tx_hash_refund` in the response is the refund ledger hash.

#### Response

```json
{
  "success": true,
  "data": {
    "policyId": "...",
    "refundAmount": "3.20",
    "refundEventId": "...",
    "status": "refunding",
    "tx_hash_refund": "ins_refund:..."
  }
}
```
