# 取得生效中保單（GET /insurance/policies/active）

只列出目前使用者狀態為 `active` 的保單。

```
GET /v1/public/insurance/policies/active
```

#### 查詢參數

| 參數             | 必填 | 預設 | 說明                      |
| -------------- | -- | -- | ----------------------- |
| `symbol`       | 否  | —  | 依永續交易對過濾，例如 `BTC-USD`   |
| `limit`        | 否  | 20 | 最大 200                  |
| `offset`       | 否  | 0  | 分頁偏移                    |
| `expireAtFrom` | 否  | —  | `expire_at` 下界，毫秒時間戳，包含 |
| `expireAtTo`   | 否  | —  | `expire_at` 上界，毫秒時間戳，包含 |

結果會依 `expireAt` 升冪排序，最早到期的保單會排在前面。

***
