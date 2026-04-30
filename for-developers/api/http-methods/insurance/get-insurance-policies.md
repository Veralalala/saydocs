---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/bao-xian/qu-de-bao-dan-lie-biao-get-insurancepolicies
---

# GET insurance/policies

List all policies for the current authenticated user (active + history).

```
GET /v1/public/insurance/policies
```

No query parameters required.

#### Response

```json
{
  "success": true,
  "data": [
    {
      "lifecycleStatus": "active",
      "displayStatus": "Active",
      "closureReason": "",
      "replacementHint": "",
      "paymentStatus": "paid",
      "tx_hash": "ins_premium:...",
      "tx_hash_refund": "",
      "policy": {
        "policyId": "...",
        "positionUid": "...",
        "insuranceType": "REVIVAL",
        "status": "active",
        "side": "buy",
        "symbol": "BTC-USD",
        "startAt": 1700000000000,
        "expireAt": 1700086400000,
        "premium": "4.00",
        "payoutAmount": "100.00",
        "payoutPercent": 100,
        "triggerPercent": 80,
        "triggerPrice": "50000.0"
      },
      "obligations": [],
      "triggerEvents": []
    }
  ]
}
```

***

### Policy Object Reference

The following fields appear in most policy responses:

| Field             | Type    | Description                                                                      |
| ----------------- | ------- | -------------------------------------------------------------------------------- |
| `policyId`        | string  | Unique policy identifier                                                         |
| `positionUid`     | string  | Associated position UID                                                          |
| `insuranceType`   | string  | `REVIVAL` or `PROFIT_DOUBLE`                                                     |
| `status`          | string  | Raw lifecycle status: `active`, `refunding`, `expired`, `triggered`, `cancelled` |
| `lifecycleStatus` | string  | Same as `status`                                                                 |
| `displayStatus`   | string  | Normalized display status                                                        |
| `side`            | string  | Position direction: `buy` or `sell`                                              |
| `symbol`          | string  | Trading symbol, e.g. `BTC-USD`                                                   |
| `startAt`         | integer | Policy start time (Unix ms)                                                      |
| `expireAt`        | integer | Planned expiry time (Unix ms)                                                    |
| `premium`         | string  | Premium paid (decimal string)                                                    |
| `payoutAmount`    | string  | Payout amount (decimal string)                                                   |
| `payoutPercent`   | integer | Payout percentage relative to position margin                                    |
| `triggerPercent`  | integer | Trigger percentage relative to entry price                                       |
| `triggerPrice`    | string  | Computed trigger price                                                           |
| `tx_hash`         | string  | Premium ledger tx hash                                                           |
| `tx_hash_refund`  | string  | Refund ledger tx hash (if applicable)                                            |
| `obligations`     | array   | Payout obligations (see below)                                                   |
| `triggerEvents`   | array   | Trigger events (see below)                                                       |

#### Obligation Object

| Field            | Type   | Description                                                                       |
| ---------------- | ------ | --------------------------------------------------------------------------------- |
| `obligationId`   | string | Unique obligation ID                                                              |
| `amount`         | string | Payout amount (decimal string)                                                    |
| `currency`       | string | Payout currency, e.g. `USD`                                                       |
| `payoutStatus`   | string | `PENDING_PAYOUT`, `PAID`, `BLOCKED_BY_SWITCH`, `PENDING_FUNDING`, `MANUAL_REVIEW` |
| `tx_hash_payout` | string | Payout ledger hash (when `payoutStatus = PAID`)                                   |

#### Trigger Event Object

| Field            | Type    | Description                                                      |
| ---------------- | ------- | ---------------------------------------------------------------- |
| `triggerEventId` | string  | Unique event ID                                                  |
| `createdAt`      | integer | Trigger time (Unix ms)                                           |
| `triggerReason`  | string  | `LIQ_PREVENT`, `INS_TAKE_PROFIT`, `EXPIRED`, `CANCELLED_*`, etc. |
