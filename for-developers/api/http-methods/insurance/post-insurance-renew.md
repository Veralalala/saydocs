---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/bao-xian/xu-bao-post-insurancerenew
---

# POST insurance/renew

Renew (replace) an existing active insurance policy with a new one.

```
POST /v1/private/insurance/renew
```

#### Request Body

| Field                    | Type    | Required | Description                                                                   |
| ------------------------ | ------- | -------- | ----------------------------------------------------------------------------- |
| `policyId`               | string  | Yes      | ID of the active policy to renew                                              |
| `durationHours`          | integer | Yes      | New policy duration. Enum: `24`, `72`, `168`                                  |
| `requestIdempotencyKey`  | string  | Yes      | Idempotency key (UUID recommended)                                            |
| `premiumLimit`           | string  | No       | Maximum acceptable premium (mutually exclusive with `acceptUnlimitedPremium`) |
| `acceptUnlimitedPremium` | boolean | No       | Accept any premium without limit (mutually exclusive with `premiumLimit`)     |
| `payoutPercent`          | integer | No       | Override default payout percentage                                            |
| `triggerPercent`         | integer | No       | Override default trigger percentage                                           |

> **Note:** On success, the old policy enters a replacement/refund flow and a new policy is created. The original `expireAt` is not extended — a new expiry is set.

#### Response

```json
{
  "success": true,
  "data": {
    "policyId": "...",
    "newPolicyId": "...",
    "oldPolicyId": "...",
    "premium": "5.00",
    "refundAmount": "2.50",
    "refundEventId": "...",
    "renewalEventId": "...",
    "payoutAmount": "100.00",
    "payoutPercent": 100,
    "triggerPercent": 80,
    "triggerPrice": "50000.0",
    "expiresAt": 1700086400000,
    "status": "active",
    "tx_hash": "ins_premium:...",
    "tx_hash_refund": "ins_refund:..."
  }
}
```

#### Response Fields

| Field                           | Type   | Description                               |
| ------------------------------- | ------ | ----------------------------------------- |
| `data.policyId` / `newPolicyId` | string | New policy ID                             |
| `data.oldPolicyId`              | string | Replaced policy ID                        |
| `data.premium`                  | string | Premium charged for the new policy        |
| `data.refundAmount`             | string | Refund amount from the old policy         |
| `data.refundEventId`            | string | Refund event identifier                   |
| `data.tx_hash`                  | string | Ledger hash for the new premium deduction |
| `data.tx_hash_refund`           | string | Ledger hash for the refund                |
