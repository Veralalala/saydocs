# 退保（POST /insurance/cancel）

取消一張生效中的保單，並發起退費。

```
POST /v1/private/insurance/cancel
```

#### 請求體

| 欄位                      | 型別     | 必填 | 說明            |
| ----------------------- | ------ | -- | ------------- |
| `policyId`              | string | 是  | 要取消的生效中保單 ID。 |
| `requestIdempotencyKey` | string | 是  | 冪等鍵。          |

> 取消後，保單狀態會從 `refunding` 進入 `cancelled`。回應中的 `tx_hash_refund` 是退費帳本雜湊。

#### 回應

```json
{
  "success": true,
  "data": {
    "policyId": "...",
    "refundAmount": "3.20",
    "refundEventId": "...",
    "status": "refunding",
    "tx_hash_refund": "ins_refund:..."
  }
}
```
