# 取消倉位保護（POST /positions/protection/cancel）

取消指定倉位的止盈、止損，或同時取消兩者。

```
POST /v1/private/exchange/positions/protection/cancel
```

### 請求體

| 欄位             | 類型     | 必填 | 說明                                            |
| -------------- | ------ | -- | --------------------------------------------- |
| `position_uid` | string | 是  | 要取消保護規則的目標倉位 ID。                              |
| `target`       | string | 是  | 取消目標。可選值為 `take_profit`、`stop_loss` 或 `both`。 |

### 回應

```json
{
  "success": true,
  "data": {
    "position": {}
  }
}
```

#### 回應欄位

| 欄位                                   | 類型      | 說明        |
| ------------------------------------ | ------- | --------- |
| `data`                               | object  | 回應結果。     |
| `data.position`                      | object  | 更新後的倉位物件。 |
| `data.position.avg_close_price`      | string  | 平倉均價。     |
| `data.position.closed_quantity`      | string  | 已平數量。     |
| `data.position.entry_price`          | string  | 開倉均價。     |
| `data.position.leverage`             | string  | 目前槓桿。     |
| `data.position.liquidation_price`    | string  | 預估強平價格。   |
| `data.position.margin`               | string  | 目前保證金。    |
| `data.position.opened_at`            | string  | 開倉時間。     |
| `data.position.positionUid`          | string  | 倉位唯一識別。   |
| `data.position.realized_pnl`         | string  | 已實現盈虧。    |
| `data.position.side`                 | string  | 倉位方向。     |
| `data.position.size`                 | string  | 目前倉位數量。   |
| `data.position.stop_loss_price`      | string  | 止損觸發價。    |
| `data.position.stop_loss_quantity`   | string  | 止損數量。     |
| `data.position.symbol`               | string  | 交易對。      |
| `data.position.take_profit_price`    | string  | 止盈觸發價。    |
| `data.position.take_profit_quantity` | string  | 止盈數量。     |
| `success`                            | boolean | 請求是否成功。   |
