# 創建訂單（POST /orders）

創建訂單。支援 `market`、`limit`、`stop_loss`、`take_profit`。

```
POST /v1/private/exchange/orders
```

### 請求體

| 欄位                       | 類型         | 必填 | 說明                                                                   |
| ------------------------ | ---------- | -- | -------------------------------------------------------------------- |
| `cost`                   | string     | 否  | 與 `quantity` 二選一。表示總成本預算，包含保證金與手續費。語義與 `/orders/by-cost` 一致。         |
| `insurances`             | object \[] | 否  | 保險列表。僅當 `order_type = market` 時可用。單次請求可附帶多個保險項。                      |
| `acceptUnlimitedPremium` | boolean    | 否  | 是否接受不設保費上限。                                                          |
| `durationHours`          | integer    | 是  | 保險持續時長，單位為小時。                                                        |
| `insuranceType`          | string     | 是  | 保險類型。                                                                |
| `payoutPercent`          | integer    | 否  | 賠付比例。                                                                |
| `premiumLimit`           | string     | 否  | 可接受的保費上限。                                                            |
| `triggerPercent`         | integer    | 否  | 觸發百分比。                                                               |
| `leverage`               | string     | 否  | 槓桿倍數。必須是大於 0 且不大於 100 的整數字串。                                         |
| `limit_price`            | string     | 否  | 限價單價格。`order_type = limit` 時必填。                                      |
| `order_type`             | string     | 是  | 訂單類型。僅支援 `market`、`limit`、`stop_loss`、`take_profit`。其中後兩者表示直接設定倉位保護。 |
| `position_uid`           | string     | 否  | 獨立設定止盈或止損時必填，用於綁定目標倉位。主訂單場景通常省略。                                     |
| `quantity`               | string     | 否  | 與 `cost` 二選一。表示下單數量，必須是正數字串。獨立止盈 / 止損僅支援 `quantity`。                 |
| `side`                   | string     | 否  | 買賣方向。主訂單場景必填，可選 `buy` 或 `sell`。獨立止盈 / 止損會依 `position_uid` 推導此值。      |
| `stop_loss_price`        | string     | 否  | 止損觸發價。`order_type = stop_loss` 時必填；主訂單場景下表示附帶的止損價。                   |
| `stop_loss_quantity`     | string     | 否  | 止損數量。僅主訂單場景有效。省略時預設等於主訂單數量。                                          |
| `symbol`                 | string     | 否  | 交易對，例如 `BTC-USD`。主訂單場景必填；獨立止盈 / 止損可透過 `position_uid` 推導。             |
| `take_profit_price`      | string     | 否  | 止盈觸發價。`order_type = take_profit` 時必填；主訂單場景下表示附帶的止盈價。                 |
| `take_profit_quantity`   | string     | 否  | 止盈數量。僅主訂單場景有效。省略時預設等於主訂單數量。                                          |

### 回應

```json
{
  "success": true,
  "data": {
    "executed": true,
    "execution_slippage_bps": "...",
    "fee": "...",
    "fill_id": "...",
    "filled_quantity": "...",
    "insurance_policies": [],
    "insurance_policy_ids": "...",
    "insurance_total_premium": "...",
    "ledger_tx_id": "...",
    "mark_price": "...",
    "order_filled_quantity": "...",
    "order_id": "...",
    "order_type": "...",
    "position_uid": "...",
    "price": "...",
    "protection_id": "...",
    "side": "...",
    "status": "...",
    "symbol": "..."
  }
}
```

#### 回應欄位

| 欄位                                       | 類型         | 說明          |
| ---------------------------------------- | ---------- | ----------- |
| `data`                                   | object     | 下單結果。       |
| `data.executed`                          | boolean    | 是否已執行。      |
| `data.execution_slippage_bps`            | string     | 執行滑點，單位為基點。 |
| `data.fee`                               | string     | 手續費。        |
| `data.fill_id`                           | string     | 成交 ID。      |
| `data.filled_quantity`                   | string     | 實際成交數量。     |
| `data.insurance_policies`                | object \[] | 關聯保險列表。     |
| `data.insurance_policies.expiresAt`      | integer    | 到期時間。       |
| `data.insurance_policies.insuranceType`  | string     | 保險類型。       |
| `data.insurance_policies.payoutAmount`   | string     | 賠付金額。       |
| `data.insurance_policies.payoutPercent`  | integer    | 賠付比例。       |
| `data.insurance_policies.policyId`       | string     | 保單 ID。      |
| `data.insurance_policies.premium`        | string     | 保費。         |
| `data.insurance_policies.triggerPercent` | integer    | 觸發百分比。      |
| `data.insurance_policies.triggerPrice`   | string     | 觸發價格。       |
| `data.insurance_policies.tx_hash`        | string     | 鏈上交易雜湊。     |
| `data.insurance_policy_ids`              | string \[] | 保險保單 ID 列表。 |
| `data.insurance_total_premium`           | string     | 總保費。        |
| `data.ledger_tx_id`                      | string     | 帳本流水 ID。    |
| `data.mark_price`                        | string     | 標記價格。       |
| `data.order_filled_quantity`             | string     | 訂單累計成交數量。   |
| `data.order_id`                          | string     | 訂單 ID。      |
| `data.order_type`                        | string     | 訂單類型。       |
| `data.position_uid`                      | string     | 關聯倉位 ID。    |
| `data.price`                             | string     | 成交價格或訂單價格。  |
| `data.protection_id`                     | string     | 倉位保護 ID。    |
| `data.side`                              | string     | 買賣方向。       |
| `data.status`                            | string     | 訂單狀態。       |
| `data.symbol`                            | string     | 交易對。        |
| `success`                                | boolean    | 請求是否成功。     |
