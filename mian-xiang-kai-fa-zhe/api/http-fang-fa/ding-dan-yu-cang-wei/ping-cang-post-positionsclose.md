# 平倉（POST /positions/close）

關閉指定倉位。支援全平和部分平倉。

```
POST /v1/private/exchange/positions/close
```

### 請求體

| 欄位                | 類型     | 必填 | 說明                                 |
| ----------------- | ------ | -- | ---------------------------------- |
| `client_close_id` | string | 否  | 當傳入 `quantity` 時建議攜帶。若傳入，必須是 UUID。 |
| `position_uid`    | string | 是  | 要平掉的目標倉位 ID。                       |
| `quantity`        | string | 否  | 平倉數量。省略表示全部平倉；傳值表示部分平倉，必須是正數字串。    |

### 回應

```json
{
  "success": true,
  "data": {
    "close_avg_price": "...",
    "closed_quantity": "...",
    "fee": "...",
    "is_full_close": true,
    "ledger_tx_id": "...",
    "pnl": "...",
    "proceeds": "...",
    "remaining_margin": "...",
    "remaining_size": "..."
  }
}
```

#### 回應欄位

| 欄位                      | 類型      | 說明         |
| ----------------------- | ------- | ---------- |
| `data`                  | object  | 平倉結果。      |
| `data.close_avg_price`  | string  | 平倉均價。      |
| `data.closed_quantity`  | string  | 已平數量。      |
| `data.fee`              | string  | 本次平倉手續費。   |
| `data.is_full_close`    | boolean | 是否為全部平倉。   |
| `data.ledger_tx_id`     | string  | 關聯帳本流水 ID。 |
| `data.pnl`              | string  | 已實現盈虧。     |
| `data.proceeds`         | string  | 平倉回收金額。    |
| `data.remaining_margin` | string  | 剩餘保證金。     |
| `data.remaining_size`   | string  | 剩餘倉位數量。    |
| `success`               | boolean | 請求是否成功。    |
