# 發起內部劃轉（POST /wallet/transfer）

在系統內向其他地址發起內部資金劃轉。

```
POST /v1/private/exchange/wallet/transfer
```

### 請求體

| 欄位            | 類型     | 必填 | 說明                      |
| ------------- | ------ | -- | ----------------------- |
| `amount`      | string | 是  | 劃轉金額，必須是符合帳本精度的正數字串。    |
| `to_address`  | string | 是  | 目標 EVM 地址，且不能與目前簽名地址相同。 |
| `transfer_id` | string | 否  | 冪等 ID。省略時由伺服器自動產生 UUID。 |

### 回應

```json
{
  "success": true,
  "data": {
    "tx_id": "..."
  }
}
```

#### 回應欄位

| 欄位           | 類型      | 說明       |
| ------------ | ------- | -------- |
| `data`       | object  | 劃轉結果。    |
| `data.tx_id` | string  | 劃轉流水 ID。 |
| `success`    | boolean | 請求是否成功。  |
