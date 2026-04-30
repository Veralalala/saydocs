# 取得續保預覽（POST /insurance/renew/preview）

```
POST /v1/public/insurance/renew/preview
```

#### 查詢參數

| 參數        | 必填 | 說明                                                             |
| --------- | -- | -------------------------------------------------------------- |
| `address` | 否  | 使用者 EVM 地址（`0x...`）。也可透過 `X-Sayfi-User-Address` 傳入，建議優先使用請求標頭。 |

#### 請求體

| 欄位               | 型別      | 必填 | 說明       |
| ---------------- | ------- | -- | -------- |
| `durationHours`  | integer | 是  | 新保單時長。   |
| `payoutPercent`  | integer | 否  | 可選的賠付比例。 |
| `policyId`       | string  | 是  | 既有保單 ID。 |
| `triggerPercent` | integer | 否  | 可選的觸發比例。 |

#### 回應

```json
{
  "success": true,
  "data": {
    "currency": "...",
    "netAmount": "...",
    "newPolicyPremium": "...",
    "policyId": "...",
    "pricedAt": 0,
    "refundAmount": "..."
  }
}
```

#### 回應欄位

| 欄位                      | 型別      | 說明       |
| ----------------------- | ------- | -------- |
| `data`                  | object  | 回應主體。    |
| `data.currency`         | string  | 幣別。      |
| `data.netAmount`        | string  | 淨額。      |
| `data.newPolicyPremium` | string  | 新保單保費。   |
| `data.policyId`         | string  | 原保單 ID。  |
| `data.pricedAt`         | integer | 計價時間。    |
| `data.refundAmount`     | string  | 原保單退費金額。 |
| `success`               | boolean | 請求是否成功。  |
