---
description: Deposit address (public).
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/qian-bao-yu-zi-jin/qu-de-chong-zhi-di-zhi-get-walletdepositaddress
---

# GET wallet/deposit-address

```
GET /v1/public/exchange/wallet/deposit-address
```

#### Query Parameters

| Parameter | Required | Description                                                                   |
| --------- | -------- | ----------------------------------------------------------------------------- |
| `chain`   | Yes      | Chain Name                                                                    |
| `asset`   | No       | Asset symbol; defaults to USDC when omitted, currently only USDC is supported |
| `address` | No       | User EVM address (0x…); option with X-Sayfi-User-Address, header preferred    |

#### Response

```json
{
  "success": true,
  "data": {
    "address": "...",
    "asset": "...",
    "chain": "...",
    "mode": "...",
    "warning": "..."
  }
}
```

#### Response Fields

| Field          | Type    | Description |
| -------------- | ------- | ----------- |
| `data`         | object  |             |
| `data.address` | string  |             |
| `data.asset`   | string  |             |
| `data.chain`   | string  |             |
| `data.mode`    | string  |             |
| `data.warning` | string  |             |
| `success`      | boolean |             |
