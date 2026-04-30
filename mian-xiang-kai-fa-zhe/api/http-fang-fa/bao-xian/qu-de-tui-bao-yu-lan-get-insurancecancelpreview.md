# 取得退保預覽（GET /insurance/cancel/preview）

```
GET /v1/public/insurance/cancel/preview
```

#### 查詢參數

| 參數         | 必填 | 說明                                                             |
| ---------- | -- | -------------------------------------------------------------- |
| `address`  | 否  | 使用者 EVM 地址（`0x...`）。也可透過 `X-Sayfi-User-Address` 傳入，建議優先使用請求標頭。 |
| `policyId` | 是  | 保單 ID，UUID。                                                    |

#### 回應

```json
{
  "success": true,
  "data": {
    "breakdown": {},
    "currency": "...",
    "policyId": "...",
    "pricedAt": 0,
    "refundAmount": "..."
  }
}
```

#### 回應欄位

| 欄位                                | 型別      | 說明                                                 |
| --------------------------------- | ------- | -------------------------------------------------- |
| `data`                            | object  | 回應主體。                                              |
| `data.breakdown`                  | object  | 退費拆解結果。                                            |
| `data.breakdown.fairBasePremium`  | string  | FairBasePremium 基礎選擇權價值中可退回的部分；會用保單建立時的價格快照重新計算。   |
| `data.breakdown.riskProfitRefund` | string  | 風險保費與利潤保費依剩餘時間乘上 `refund_risk_profit_pct` 後可退回的金額。 |
| `data.currency`                   | string  | 幣別。                                                |
| `data.policyId`                   | string  | 保單 ID。                                             |
| `data.pricedAt`                   | integer | 計價時間。                                              |
| `data.refundAmount`               | string  | 退費金額。                                              |
| `success`                         | boolean | 請求是否成功。                                            |
