# 取得資金規則（GET /funds/rules）

返回目前支援的充值鏈、提現鏈、資產，以及提現精度限制。

```
GET /v1/public/exchange/funds/rules
```

此介面不需要查詢參數。

### 回應

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

#### 回應欄位

| 欄位                                                   | 類型         | 說明            |
| ---------------------------------------------------- | ---------- | ------------- |
| `data`                                               | object     | 資金規則物件。       |
| `data.deposit_supported_assets`                      | object \[] | 支援充值的資產列表。    |
| `data.deposit_supported_assets.asset`                | string     | 資產符號。         |
| `data.deposit_supported_assets.chain`                | string     | 對應鏈名稱。        |
| `data.deposit_supported_assets.decimals`             | integer    | 資產精度。         |
| `data.deposit_supported_assets.token_address`        | string     | 代幣合約地址。       |
| `data.deposit_supported_chains`                      | string \[] | 支援充值的鏈列表。     |
| `data.withdraw_amount_max_decimals`                  | integer    | 提現金額允許的小數位上限。 |
| `data.withdraw_supported_assets`                     | object \[] | 支援提現的資產列表。    |
| `data.withdraw_supported_assets.asset`               | string     | 資產符號。         |
| `data.withdraw_supported_assets.chain`               | string     | 對應鏈名稱。        |
| `data.withdraw_supported_assets.decimals`            | integer    | 資產精度。         |
| `data.withdraw_supported_assets.token_address`       | string     | 代幣合約地址。       |
| `data.withdraw_supported_assets.withdraw_fixed_fee`  | string     | 固定提現手續費。      |
| `data.withdraw_supported_assets.withdraw_min_amount` | string     | 最小提現金額。       |
| `data.withdraw_supported_chains`                     | string \[] | 支援提現的鏈列表。     |
| `success`                                            | boolean    | 請求是否成功。       |
