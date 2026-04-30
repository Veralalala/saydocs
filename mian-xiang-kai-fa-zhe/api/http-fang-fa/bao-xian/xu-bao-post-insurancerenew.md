# 續保（POST /insurance/renew）

用一張新保單替換現有生效中的保單。

```
POST /v1/private/insurance/renew
```

#### 請求體

| 欄位                       | 型別      | 必填 | 說明                                      |
| ------------------------ | ------- | -- | --------------------------------------- |
| `policyId`               | string  | 是  | 要續保的生效中保單 ID。                           |
| `durationHours`          | integer | 是  | 新保單時長。枚舉：`24`、`72`、`168`。               |
| `requestIdempotencyKey`  | string  | 是  | 冪等鍵，建議使用 UUID。                          |
| `premiumLimit`           | string  | 否  | 可接受的最大保費。與 `acceptUnlimitedPremium` 互斥。 |
| `acceptUnlimitedPremium` | boolean | 否  | 是否接受不限額保費。與 `premiumLimit` 互斥。          |
| `payoutPercent`          | integer | 否  | 覆蓋預設賠付比例。                               |
| `triggerPercent`         | integer | 否  | 覆蓋預設觸發比例。                               |

> **說明：** 成功後，舊保單會進入替換與退費流程，同時建立新保單。原本的 `expireAt` 不會順延，而是重新產生新的到期時間。

#### 回應

```json
{
  "success": true,
  "data": {
    "policyId": "...",
    "newPolicyId": "...",
    "oldPolicyId": "...",
    "premium": "5.00",
    "refundAmount": "2.50",
    "refundEventId": "...",
    "renewalEventId": "...",
    "payoutAmount": "100.00",
    "payoutPercent": 100,
    "triggerPercent": 80,
    "triggerPrice": "50000.0",
    "expiresAt": 1700086400000,
    "status": "active",
    "tx_hash": "ins_premium:...",
    "tx_hash_refund": "ins_refund:..."
  }
}
```

#### 回應欄位

| 欄位                              | 型別     | 說明          |
| ------------------------------- | ------ | ----------- |
| `data.policyId` / `newPolicyId` | string | 新保單 ID。     |
| `data.oldPolicyId`              | string | 被替換的舊保單 ID。 |
| `data.premium`                  | string | 新保單扣除的保費。   |
| `data.refundAmount`             | string | 舊保單退回的金額。   |
| `data.refundEventId`            | string | 退費事件 ID。    |
| `data.tx_hash`                  | string | 新保費扣款的帳本雜湊。 |
| `data.tx_hash_refund`           | string | 退費帳本雜湊。     |
