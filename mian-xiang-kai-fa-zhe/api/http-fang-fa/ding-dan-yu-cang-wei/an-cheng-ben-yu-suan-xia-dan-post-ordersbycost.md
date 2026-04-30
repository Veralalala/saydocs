# 按成本預算下單（POST /orders/by-cost）

按總成本預算下單。適合先確定總支出，再由系統反算數量。

```
POST /v1/private/exchange/orders/by-cost
```

### 請求體

| 欄位                     | 類型     | 必填 | 說明                                        |
| ---------------------- | ------ | -- | ----------------------------------------- |
| `cost`                 | string | 是  | 使用者可接受的總成本，包含保證金與手續費。                     |
| `leverage`             | string | 否  | 槓桿倍數。必須是大於 0 且不大於 100 的整數字串。              |
| `limit_price`          | string | 否  | 限價單價格。`order_type = limit` 時必填。           |
| `order_type`           | string | 是  | 訂單類型。僅支援 `market` 和 `limit`。不支援獨立止盈 / 止損。 |
| `position_uid`         | string | 否  | 預留欄位。目前成本預算單通常省略。                         |
| `side`                 | string | 是  | 買賣方向。僅支援 `buy` 或 `sell`。                  |
| `stop_loss_price`      | string | 否  | 附帶止損價格。僅主訂單場景有效。                          |
| `stop_loss_quantity`   | string | 否  | 附帶止損數量。省略時預設等於系統反算出的主訂單數量。                |
| `symbol`               | string | 是  | 交易對，例如 `BTC-USD`。                         |
| `take_profit_price`    | string | 否  | 附帶止盈價格。僅主訂單場景有效。                          |
| `take_profit_quantity` | string | 否  | 附帶止盈數量。省略時預設等於系統反算出的主訂單數量。                |

### 回應

```json
{
  "success": true,
  "data": {
    "computed_fee": "...",
    "computed_margin": "...",
    "computed_quantity": "...",
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
    "reference_price": "...",
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
| `data.computed_fee`                      | string     | 系統反算出的手續費。  |
| `data.computed_margin`                   | string     | 系統反算出的保證金。  |
| `data.computed_quantity`                 | string     | 系統反算出的下單數量。 |
| `data.executed`                          | boolean    | 是否已執行。      |
| `data.execution_slippage_bps`            | string     | 執行滑點，單位為基點。 |
| `data.fee`                               | string     | 實際手續費。      |
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
| `data.reference_price`                   | string     | 反算使用的參考價格。  |
| `data.side`                              | string     | 買賣方向。       |
| `data.status`                            | string     | 訂單狀態。       |
| `data.symbol`                            | string     | 交易對。        |
| `success`                                | boolean    | 請求是否成功。     |
