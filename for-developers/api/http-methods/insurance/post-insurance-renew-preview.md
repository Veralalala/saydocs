---
description: Renew preview (public).
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/bao-xian/qu-de-xu-bao-yu-lan-post-insurancerenewpreview
---

# POST insurance/renew/preview

```
POST /v1/public/insurance/renew/preview
```

#### Query Parameters

| Parameter | Required | Description                                                                  |
| --------- | -------- | ---------------------------------------------------------------------------- |
| `address` | No       | User EVM address (0x...); option with X-Sayfi-User-Address, header preferred |

#### Request Body

| Field            | Type    | Required | Description |
| ---------------- | ------- | -------- | ----------- |
| `durationHours`  | integer | Yes      |             |
| `payoutPercent`  | integer | No       |             |
| `policyId`       | string  | Yes      |             |
| `triggerPercent` | integer | No       |             |

#### Response

```json
{
  "success": true,
  "data": {
    "currency": "...",
    "netAmount": "...",
    "newPolicyPremium": "...",
    "policyId": "...",
    "pricedAt": 0,
    "refundAmount": "..."
  }
}
```

#### Response Fields

| Field                   | Type    | Description |
| ----------------------- | ------- | ----------- |
| `data`                  | object  |             |
| `data.currency`         | string  |             |
| `data.netAmount`        | string  |             |
| `data.newPolicyPremium` | string  |             |
| `data.policyId`         | string  |             |
| `data.pricedAt`         | integer |             |
| `data.refundAmount`     | string  |             |
| `success`               | boolean |             |
