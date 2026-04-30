# 建立提現（POST /wallet/withdrawals）

建立一筆提現請求。

```
POST /v1/private/exchange/wallet/withdrawals
```

### 請求體

| 欄位                   | 類型     | 必填 | 說明                               |
| -------------------- | ------ | -- | -------------------------------- |
| `amount`             | string | 是  | 提現金額。必須是正數字串，並符合手續費、最小提現金額與精度限制。 |
| `asset`              | string | 否  | 資產符號。省略時預設為 `USDC`。目前僅支援 `USDC`。 |
| `chain`              | string | 是  | 目標鏈名稱，必須在伺服器允許列表中。               |
| `client_withdraw_id` | string | 否  | 冪等 ID。若傳入，必須是 UUID。              |
| `to_address`         | string | 是  | 提現目標地址。必須是有效的 EVM 地址，且不能為零地址。    |
| `token_address`      | string | 是  | 所選鏈上的代幣合約地址。必須是有效的 EVM 合約地址。     |

### 回應

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

#### 回應欄位

| 欄位                | 類型      | 說明         |
| ----------------- | ------- | ---------- |
| `data`            | object  | 提現申請結果。    |
| `data.hold_tx_id` | string  | 資金凍結流水 ID。 |
| `data.request_id` | string  | 提現請求 ID。   |
| `data.status`     | string  | 提現狀態。      |
| `success`         | boolean | 請求是否成功。    |
