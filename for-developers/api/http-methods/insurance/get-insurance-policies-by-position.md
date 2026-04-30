---
description: Policies by position (public).
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/bao-xian/yi-cang-wei-cha-xun-bao-dan-get-insurancepoliciesbyposition
---

# GET insurance/policies/by-position

```
GET /v1/public/insurance/policies/by-position
```

#### Query Parameters

| Parameter      | Required | Description                                                                  |
| -------------- | -------- | ---------------------------------------------------------------------------- |
| `address`      | No       | User EVM address (0x...); option with X-Sayfi-User-Address, header preferred |
| `positionId`   | Yes      | Position ID (UUID)                                                           |
| `limit`        | No       | Number of bars per page, default 20, maximum 200                             |
| `offset`       | No       | Offset, default 0                                                            |
| `expireAtFrom` | No       | Optional, expire\_at lower limit (inclusive), milliseconds                   |
| `expireAtTo`   | No       | Optional, upper expire\_at limit (inclusive), milliseconds                   |

#### Response

```json
{
  "success": true,
  "data": {
    "items": [],
    "limit": 0,
    "offset": 0,
    "sort": "...",
    "timeAxis": "...",
    "total": 0
  }
}
```

#### Response Fields

| Field                                     | Type       | Description                                                                                            |
| ----------------------------------------- | ---------- | ------------------------------------------------------------------------------------------------------ |
| `data`                                    | object     |                                                                                                        |
| `data.items`                              | object \[] |                                                                                                        |
| `data.items.closureReason`                | string     |                                                                                                        |
| `data.items.displayStatus`                | string     |                                                                                                        |
| `data.items.expireAt`                     | integer    |                                                                                                        |
| `data.items.insuranceType`                | string     |                                                                                                        |
| `data.items.lifecycleStatus`              | string     |                                                                                                        |
| `data.items.obligations`                  | object \[] |                                                                                                        |
| `data.items.obligations.amount`           | string     | Payment amount (string format to avoid loss of precision)                                              |
| `data.items.obligations.currency`         | string     | Payment currency, e.g. USD                                                                             |
| `data.items.obligations.obligationId`     | string     | Unique identifier of the indemnity obligation                                                          |
| `data.items.obligations.payoutStatus`     | string     | Payment execution status: pending\_payout, paid, blocked\_BY\_switch, pending\_funding, manual\_review |
| `data.items.obligations.tx_hash_payout`   | string     |                                                                                                        |
| `data.items.paymentStatus`                | string     |                                                                                                        |
| `data.items.payoutAmount`                 | string     |                                                                                                        |
| `data.items.payoutPercent`                | integer    |                                                                                                        |
| `data.items.policy`                       | object     |                                                                                                        |
| `data.items.policy.expireAt`              | integer    | Insurance Expiration Timestamp (ms)                                                                    |
| `data.items.policy.insuranceType`         | string     | Insurance type: revival, profit\_double, etc.                                                          |
| `data.items.policy.payoutAmount`          | string     | Payment amount (string format to avoid loss of precision)                                              |
| `data.items.policy.payoutPercent`         | integer    | Payout Percentage, Relative to Position Margin                                                         |
| `data.items.policy.policyId`              | string     | Insurance Policy Unique Identifier                                                                     |
| `data.items.policy.positionUid`           | string     | Unique identifier of the associated trade position                                                     |
| `data.items.policy.premium`               | string     | Premium amount (string format to avoid loss of precision)                                              |
| `data.items.policy.side`                  | string     | Position Direction: buy or sell                                                                        |
| `data.items.policy.startAt`               | integer    | Insurance Effective Timestamp (ms)                                                                     |
| `data.items.policy.status`                | string     | Lifecycle status: active, refunding, expired, triggered, cancelled                                     |
| `data.items.policy.symbol`                | string     | Symbols that are the subject of the transaction, such as BTC-USD                                       |
| `data.items.policy.triggerPercent`        | integer    | Trigger Percentage Relative to Entry Price                                                             |
| `data.items.policy.triggerPrice`          | string     | Trigger price                                                                                          |
| `data.items.policyId`                     | string     |                                                                                                        |
| `data.items.positionUid`                  | string     |                                                                                                        |
| `data.items.premium`                      | string     |                                                                                                        |
| `data.items.refundAmount`                 | string     |                                                                                                        |
| `data.items.refundCreatedAt`              | integer    |                                                                                                        |
| `data.items.refundCurrency`               | string     |                                                                                                        |
| `data.items.refundEventId`                | string     |                                                                                                        |
| `data.items.refundResolvedAt`             | integer    |                                                                                                        |
| `data.items.replacementHint`              | string     |                                                                                                        |
| `data.items.side`                         | string     |                                                                                                        |
| `data.items.startAt`                      | integer    |                                                                                                        |
| `data.items.status`                       | string     |                                                                                                        |
| `data.items.symbol`                       | string     |                                                                                                        |
| `data.items.triggerEvents`                | object \[] |                                                                                                        |
| `data.items.triggerEvents.createdAt`      | integer    | Trigger Timestamp (ms)                                                                                 |
| `data.items.triggerEvents.triggerEventId` | string     | Trigger Event Unique Identifier                                                                        |
| `data.items.triggerEvents.triggerReason`  | string     | Triggered by: LIQ\_prevent, ins\_take\_profile, expired, cancelled\_\*, etc.                           |
| `data.items.triggerPercent`               | integer    |                                                                                                        |
| `data.items.triggerPrice`                 | string     |                                                                                                        |
| `data.items.tx_hash`                      | string     |                                                                                                        |
| `data.items.tx_hash_refund`               | string     |                                                                                                        |
| `data.limit`                              | integer    |                                                                                                        |
| `data.offset`                             | integer    |                                                                                                        |
| `data.sort`                               | string     |                                                                                                        |
| `data.timeAxis`                           | string     |                                                                                                        |
| `data.total`                              | integer    |                                                                                                        |
| `success`                                 | boolean    |                                                                                                        |
