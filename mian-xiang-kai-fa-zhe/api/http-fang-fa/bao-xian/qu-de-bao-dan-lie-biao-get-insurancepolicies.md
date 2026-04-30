# 取得保單列表（GET /insurance/policies）

列出目前驗權使用者的全部保單，包含生效中與歷史保單。

```
GET /v1/public/insurance/policies
```

不需要查詢參數。

#### 回應

```json
{
  "success": true,
  "data": [
    {
      "lifecycleStatus": "active",
      "displayStatus": "Active",
      "closureReason": "",
      "replacementHint": "",
      "paymentStatus": "paid",
      "tx_hash": "ins_premium:...",
      "tx_hash_refund": "",
      "policy": {
        "policyId": "...",
        "positionUid": "...",
        "insuranceType": "REVIVAL",
        "status": "active",
        "side": "buy",
        "symbol": "BTC-USD",
        "startAt": 1700000000000,
        "expireAt": 1700086400000,
        "premium": "4.00",
        "payoutAmount": "100.00",
        "payoutPercent": 100,
        "triggerPercent": 80,
        "triggerPrice": "50000.0"
      },
      "obligations": [],
      "triggerEvents": []
    }
  ]
}
```

***

### 保單物件說明

以下欄位會出現在多數保單回應中：

| 欄位                | 型別      | 說明                                                               |
| ----------------- | ------- | ---------------------------------------------------------------- |
| `policyId`        | string  | 保單唯一識別碼。                                                         |
| `positionUid`     | string  | 關聯倉位 UID。                                                        |
| `insuranceType`   | string  | `REVIVAL` 或 `PROFIT_DOUBLE`。                                     |
| `status`          | string  | 原始生命週期狀態：`active`、`refunding`、`expired`、`triggered`、`cancelled`。 |
| `lifecycleStatus` | string  | 與 `status` 相同。                                                   |
| `displayStatus`   | string  | 正規化後的顯示狀態。                                                       |
| `side`            | string  | 倉位方向：`buy` 或 `sell`。                                             |
| `symbol`          | string  | 交易對，例如 `BTC-USD`。                                                |
| `startAt`         | integer | 保單開始時間，Unix 毫秒。                                                  |
| `expireAt`        | integer | 預計到期時間，Unix 毫秒。                                                  |
| `premium`         | string  | 已支付保費，十進位字串。                                                     |
| `payoutAmount`    | string  | 賠付金額，十進位字串。                                                      |
| `payoutPercent`   | integer | 相對於倉位保證金的賠付比例。                                                   |
| `triggerPercent`  | integer | 相對於開倉價的觸發比例。                                                     |
| `triggerPrice`    | string  | 計算後的觸發價格。                                                        |
| `tx_hash`         | string  | 保費帳本交易雜湊。                                                        |
| `tx_hash_refund`  | string  | 退費帳本交易雜湊，如適用。                                                    |
| `obligations`     | array   | 賠付義務列表，見下方。                                                      |
| `triggerEvents`   | array   | 觸發事件列表，見下方。                                                      |

#### 賠付義務物件

| 欄位               | 型別     | 說明                                                                             |
| ---------------- | ------ | ------------------------------------------------------------------------------ |
| `obligationId`   | string | 賠付義務唯一 ID。                                                                     |
| `amount`         | string | 賠付金額，十進位字串。                                                                    |
| `currency`       | string | 賠付幣別，例如 `USD`。                                                                 |
| `payoutStatus`   | string | `PENDING_PAYOUT`、`PAID`、`BLOCKED_BY_SWITCH`、`PENDING_FUNDING`、`MANUAL_REVIEW`。 |
| `tx_hash_payout` | string | 賠付帳本雜湊，當 `payoutStatus = PAID` 時可用。                                            |

#### 觸發事件物件

| 欄位               | 型別      | 說明                                                          |
| ---------------- | ------- | ----------------------------------------------------------- |
| `triggerEventId` | string  | 事件唯一 ID。                                                    |
| `createdAt`      | integer | 觸發時間，Unix 毫秒。                                               |
| `triggerReason`  | string  | 例如 `LIQ_PREVENT`、`INS_TAKE_PROFIT`、`EXPIRED`、`CANCELLED_*`。 |
