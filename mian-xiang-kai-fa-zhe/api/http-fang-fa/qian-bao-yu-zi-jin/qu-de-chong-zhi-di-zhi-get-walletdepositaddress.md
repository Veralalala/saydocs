# 取得充值地址（GET /wallet/deposit-address）

返回指定鏈與資產的充值地址。

```
GET /v1/public/exchange/wallet/deposit-address
```

### 查詢參數

| 參數        | 必填 | 說明                                                                  |
| --------- | -- | ------------------------------------------------------------------- |
| `chain`   | 是  | 鏈名稱。                                                                |
| `asset`   | 否  | 資產符號。省略時預設為 `USDC`。目前僅支援 `USDC`。                                    |
| `address` | 否  | 使用者 EVM 地址，格式為 `0x...`。也可透過 `X-Sayfi-User-Address` 請求標頭傳入，優先使用請求標頭。 |

### 回應

```json
{
  "success": true,
  "data": {
    "address": "...",
    "asset": "...",
    "chain": "...",
    "mode": "...",
    "warning": "..."
  }
}
```

#### 回應欄位

| 欄位             | 類型      | 說明         |
| -------------- | ------- | ---------- |
| `data`         | object  | 充值地址資訊。    |
| `data.address` | string  | 充值地址。      |
| `data.asset`   | string  | 資產符號。      |
| `data.chain`   | string  | 鏈名稱。       |
| `data.mode`    | string  | 充值模式。      |
| `data.warning` | string  | 風險提示或補充說明。 |
| `success`      | boolean | 請求是否成功。    |
