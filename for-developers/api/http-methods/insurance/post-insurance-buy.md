---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/bao-xian/gou-mai-bao-xian-post-insurancebuy
---

# POST insurance/buy

Purchase insurance for an existing open position.

```
POST /v1/private/insurance/buy
```

#### Request Body

| Field                    | Type    | Required | Description                      |
| ------------------------ | ------- | -------- | -------------------------------- |
| `positionUid`            | string  | Yes      | Position UID (UUID)              |
| `insuranceType`          | string  | Yes      | Enum: `REVIVAL`, `PROFIT_DOUBLE` |
| `durationHours`          | integer | Yes      | Enum: `24`, `72`, `168`          |
| `payoutPercent`          | integer | Yes      | Payout percentage                |
| `triggerPercent`         | integer | Yes      | Trigger percentage               |
| `requestIdempotencyKey`  | string  | Yes      | Idempotency key                  |
| `premiumLimit`           | string  | No       | Max acceptable premium           |
| `acceptUnlimitedPremium` | boolean | No       | Accept unlimited premium         |

> The server re-prices in real time at execution; it does not rely on a prior quote result. `premiumLimit` and `acceptUnlimitedPremium` are mutually exclusive.

#### Response

```json
{
  "success": true,
  "data": {
    "policyId": "...",
    "newPolicyId": "...",
    "premium": "4.00",
    "payoutAmount": "100.00",
    "payoutPercent": 100,
    "triggerPercent": 80,
    "triggerPrice": "50000.0",
    "expiresAt": 1700086400000,
    "status": "active",
    "tx_hash": "ins_premium:..."
  }
}
```

***
