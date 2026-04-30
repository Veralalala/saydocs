# 取消訂單（POST /orders/{id}/cancel）

```
POST /v1/private/exchange/orders/{id}/cancel
```

### 路徑參數

| 參數   | 必填 | 說明     |
| ---- | -- | ------ |
| `id` | 是  | 訂單 ID。 |

### 回應

```json
{
  "success": true,
  "data": {
    "status": "..."
  }
}
```

#### 回應欄位

| 欄位            | 類型      | 說明      |
| ------------- | ------- | ------- |
| `data`        | object  | 取消結果。   |
| `data.status` | string  | 訂單最新狀態。 |
| `success`     | boolean | 請求是否成功。 |
