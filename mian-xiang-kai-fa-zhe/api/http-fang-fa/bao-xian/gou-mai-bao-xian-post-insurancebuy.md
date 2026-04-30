# 購買保險（POST /insurance/buy）

為現有持倉購買保險

```
POST /v1/private/insurance/buy
```

#### 請求體

| 欄位                       | 型別      | 必填 | 說明                            |
| ------------------------ | ------- | -- | ----------------------------- |
| `positionUid`            | string  | 是  | 仓位 UID，UUID。                  |
| `insuranceType`          | string  | 是  | 枚舉：`REVIVAL`、`PROFIT_DOUBLE`。 |
| `durationHours`          | integer | 是  | 枚舉：`24`、`72`、`168`。           |
| `payoutPercent`          | integer | 是  | 賠付比例。                         |
| `triggerPercent`         | integer | 是  | 觸發比例。                         |
| `requestIdempotencyKey`  | string  | 是  | 冪等鍵。                          |
| `premiumLimit`           | string  | 否  | 可接受的最大保費。                     |
| `acceptUnlimitedPremium` | boolean | 否  | 是否接受不限額保費。                    |

> 伺服器會在執行時即時重新定價，不依賴之前的報價結果。`premiumLimit` 與 `acceptUnlimitedPremium` 互斥。

#### 回應

```json
{
  "success": true,
  "data": {
    "policyId": "...",
    "newPolicyId": "...",
    "premium": "4.00",
    "payoutAmount": "100.00",
    "payoutPercent": 100,
    "triggerPercent": 80,
    "triggerPrice": "50000.0",
    "expiresAt": 1700086400000,
    "status": "active",
    "tx_hash": "ins_premium:..."
  }
}
```

***
