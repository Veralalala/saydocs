# 取得退費事件（GET /insurance/refund-events）

```
GET /v1/public/insurance/refund-events
```

#### 查詢參數

| 參數        | 必填 | 說明                                                             |
| --------- | -- | -------------------------------------------------------------- |
| `address` | 否  | 使用者 EVM 地址（`0x...`）。也可透過 `X-Sayfi-User-Address` 傳入，建議優先使用請求標頭。 |
| `limit`   | 否  | 每頁返回筆數，預設 20，最大 200。                                           |
| `offset`  | 否  | 分頁偏移，預設 0。                                                     |

#### 回應

```json
{
  "success": true,
  "data": {
    "items": [],
    "limit": 0,
    "offset": 0,
    "total": 0
  }
}
```

#### 回應欄位

| 欄位                               | 型別         | 說明          |
| -------------------------------- | ---------- | ----------- |
| `data`                           | object     | 回應主體。       |
| `data.items`                     | object \[] | 退費事件列表。     |
| `data.items.createdAt`           | integer    | 建立時間。       |
| `data.items.currency`            | string     | 幣別。         |
| `data.items.policyId`            | string     | 保單 ID。      |
| `data.items.reason`              | string     | 退費原因。       |
| `data.items.refundAmount`        | string     | 退費金額。       |
| `data.items.refundEventId`       | string     | 退費事件 ID。    |
| `data.items.replacementPolicyId` | string     | 替換後的新保單 ID。 |
| `data.items.resolvedAt`          | integer    | 完成時間。       |
| `data.items.tx_hash_refund`      | string     | 退費帳本交易雜湊。   |
| `data.limit`                     | integer    | 每頁筆數。       |
| `data.offset`                    | integer    | 分頁偏移。       |
| `data.total`                     | integer    | 總筆數。        |
| `success`                        | boolean    | 請求是否成功。     |
