---
description: Create withdrawal.
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/qian-bao-yu-zi-jin/jian-li-ti-xian-post-walletwithdrawals
---

# POST wallet/withdrawals

```
POST /v1/private/exchange/wallet/withdrawals
```

#### Request Body

| Field                | Type   | Required | Description                                                                                                                        |
| -------------------- | ------ | -------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `amount`             | string | Yes      | Amount must be a positive number string and meet the withdrawal fee, minimum withdrawal amount, and decimal precision constraints. |
| `asset`              | string | No       | Asset defaults to USDC when omitted; only USDC withdrawals are supported at current runtime.                                       |
| `chain`              | string | Yes      | Chain represents the target chain, and the value must be in the server-side allow list.                                            |
| `client_withdraw_id` | string | No       | ClientWithdrawID is an optional idempotent key; it must be a UUID when passed in.                                                  |
| `to_address`         | string | Yes      | ToAddress must be a valid EVM address and cannot be zero.                                                                          |
| `token_address`      | string | Yes      | TokenAddress must be a valid EVM token contract address on the selected chain.                                                     |

#### Response

```json
{
  "success": true,
  "data": {
    "hold_tx_id": "...",
    "request_id": "...",
    "status": "..."
  }
}
```

#### Response Fields

| Field             | Type    | Description |
| ----------------- | ------- | ----------- |
| `data`            | object  |             |
| `data.hold_tx_id` | string  |             |
| `data.request_id` | string  |             |
| `data.status`     | string  |             |
| `success`         | boolean |             |
