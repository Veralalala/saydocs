---
description: Deposit / withdraw rules (public).
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/qian-bao-yu-zi-jin/qu-de-zi-jin-gui-ze-get-fundsrules
---

# GET funds/rules

```
GET /v1/public/exchange/funds/rules
```

No query parameters required.

#### Response

```json
{
  "success": true,
  "data": {
    "deposit_supported_assets": [],
    "deposit_supported_chains": "...",
    "withdraw_amount_max_decimals": 0,
    "withdraw_supported_assets": [],
    "withdraw_supported_chains": "..."
  }
}
```

#### Response Fields

| Field                                                | Type       | Description |
| ---------------------------------------------------- | ---------- | ----------- |
| `data`                                               | object     |             |
| `data.deposit_supported_assets`                      | object \[] |             |
| `data.deposit_supported_assets.asset`                | string     |             |
| `data.deposit_supported_assets.chain`                | string     |             |
| `data.deposit_supported_assets.decimals`             | integer    |             |
| `data.deposit_supported_assets.token_address`        | string     |             |
| `data.deposit_supported_chains`                      | string \[] |             |
| `data.withdraw_amount_max_decimals`                  | integer    |             |
| `data.withdraw_supported_assets`                     | object \[] |             |
| `data.withdraw_supported_assets.asset`               | string     |             |
| `data.withdraw_supported_assets.chain`               | string     |             |
| `data.withdraw_supported_assets.decimals`            | integer    |             |
| `data.withdraw_supported_assets.token_address`       | string     |             |
| `data.withdraw_supported_assets.withdraw_fixed_fee`  | string     |             |
| `data.withdraw_supported_assets.withdraw_min_amount` | string     |             |
| `data.withdraw_supported_chains`                     | string \[] |             |
| `success`                                            | boolean    |             |
