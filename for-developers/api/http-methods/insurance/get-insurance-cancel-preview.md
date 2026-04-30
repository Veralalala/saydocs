---
description: Cancel refund preview (public).
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/bao-xian/qu-de-tui-bao-yu-lan-get-insurancecancelpreview
---

# GET insurance/cancel/preview

```
GET /v1/public/insurance/cancel/preview
```

#### Query Parameters

| Parameter  | Required | Description                                                                  |
| ---------- | -------- | ---------------------------------------------------------------------------- |
| `address`  | No       | User EVM address (0x...); option with X-Sayfi-User-Address, header preferred |
| `policyId` | Yes      | Policy ID (UUID)                                                             |

#### Response

```json
{
  "success": true,
  "data": {
    "breakdown": {},
    "currency": "...",
    "policyId": "...",
    "pricedAt": 0,
    "refundAmount": "..."
  }
}
```

#### Response Fields

| Field                             | Type    | Description                                                                                                                                                           |
| --------------------------------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `data`                            | object  |                                                                                                                                                                       |
| `data.breakdown`                  | object  |                                                                                                                                                                       |
| `data.breakdown.fairBasePremium`  | string  | The refundable portion of the FairBasePremium base option value (Black-Scholes Fair Base Premium); recalculated using the price snapshot when the policy was created. |
| `data.breakdown.riskProfitRefund` | string  | RiskProfitRefund The amount returned after the risk premium and profit premium are multiplied by refund\_risk\_profit\_pct in proportion to the remaining time.       |
| `data.currency`                   | string  |                                                                                                                                                                       |
| `data.policyId`                   | string  |                                                                                                                                                                       |
| `data.pricedAt`                   | integer |                                                                                                                                                                       |
| `data.refundAmount`               | string  |                                                                                                                                                                       |
| `success`                         | boolean |                                                                                                                                                                       |
