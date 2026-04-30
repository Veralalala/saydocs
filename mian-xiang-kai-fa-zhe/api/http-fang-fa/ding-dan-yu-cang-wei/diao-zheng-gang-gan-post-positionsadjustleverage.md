# 調整槓桿（POST /positions/adjust-leverage）

調整指定倉位的逐倉槓桿。

```
POST /v1/private/exchange/positions/adjust-leverage
```

### 請求體

| 欄位                 | 類型     | 必填 | 說明                               |
| ------------------ | ------ | -- | -------------------------------- |
| `client_adjust_id` | string | 是  | 調整請求 ID，必須是 UUID。                |
| `position_uid`     | string | 是  | 目標倉位的唯一識別。                       |
| `target_leverage`  | string | 是  | 目標槓桿值，必須是正整數字串，且不能超過目前執行環境允許的上限。 |

### 回應

```json
{
  "success": true,
  "data": {
    "ledger_tx_id": "...",
    "leverage": "...",
    "liquidation_price": "...",
    "margin": "...",
    "position_uid": "..."
  }
}
```

#### 回應欄位

| 欄位                       | 類型      | 說明          |
| ------------------------ | ------- | ----------- |
| `data`                   | object  | 調整結果。       |
| `data.ledger_tx_id`      | string  | 關聯帳本流水 ID。  |
| `data.leverage`          | string  | 調整後的槓桿。     |
| `data.liquidation_price` | string  | 調整後的預估強平價格。 |
| `data.margin`            | string  | 調整後的保證金。    |
| `data.position_uid`      | string  | 倉位唯一識別。     |
| `success`                | boolean | 請求是否成功。     |
