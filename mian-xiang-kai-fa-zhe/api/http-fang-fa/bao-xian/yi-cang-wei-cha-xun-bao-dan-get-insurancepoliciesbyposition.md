# 依倉位查詢保單（GET /insurance/policies/by-position）

```
GET /v1/public/insurance/policies/by-position
```

#### 查詢參數

| 參數             | 必填 | 說明                                                          |
| -------------- | -- | ----------------------------------------------------------- |
| `address`      | 否  | 使用者 EVM 地址（`0x...`）；也可透過 `X-Sayfi-User-Address` 傳入，建議優先使用標頭 |
| `positionId`   | 是  | 倉位 ID（UUID）                                                 |
| `limit`        | 否  | 每頁筆數，預設 20，最大 200                                           |
| `offset`       | 否  | 偏移量，預設 0                                                    |
| `expireAtFrom` | 否  | 可選，`expire_at` 下界，包含，毫秒                                     |
| `expireAtTo`   | 否  | 可選，`expire_at` 上界，包含，毫秒                                     |

#### 回應

```json
{
  "success": true,
  "data": {
    "items": [],
    "limit": 0,
    "offset": 0,
    "sort": "...",
    "timeAxis": "...",
    "total": 0
  }
}
```

#### 回應欄位

| 欄位                                        | 型別         | 說明                                                                                       |
| ----------------------------------------- | ---------- | ---------------------------------------------------------------------------------------- |
| `data`                                    | object     | 回應主體。                                                                                    |
| `data.items`                              | object \[] | 保單列表。                                                                                    |
| `data.items.obligations.amount`           | string     | 賠付金額，使用字串避免精度損失。                                                                         |
| `data.items.obligations.currency`         | string     | 賠付幣別，例如 USD。                                                                             |
| `data.items.obligations.obligationId`     | string     | 賠付義務唯一識別碼。                                                                               |
| `data.items.obligations.payoutStatus`     | string     | 賠付執行狀態，例如 `pending_payout`、`paid`、`blocked_by_switch`、`pending_funding`、`manual_review`。 |
| `data.items.policy.expireAt`              | integer    | 保險到期時間戳，毫秒。                                                                              |
| `data.items.policy.insuranceType`         | string     | 保險類型，例如 `REVIVAL`、`PROFIT_DOUBLE`。                                                       |
| `data.items.policy.payoutAmount`          | string     | 賠付金額。                                                                                    |
| `data.items.policy.payoutPercent`         | integer    | 相對於倉位保證金的賠付比例。                                                                           |
| `data.items.policy.policyId`              | string     | 保單唯一識別碼。                                                                                 |
| `data.items.policy.positionUid`           | string     | 關聯倉位唯一識別碼。                                                                               |
| `data.items.policy.premium`               | string     | 保費金額。                                                                                    |
| `data.items.policy.side`                  | string     | 倉位方向，`buy` 或 `sell`。                                                                     |
| `data.items.policy.startAt`               | integer    | 保險生效時間戳，毫秒。                                                                              |
| `data.items.policy.status`                | string     | 生命週期狀態，例如 `active`、`refunding`、`expired`、`triggered`、`cancelled`。                        |
| `data.items.policy.symbol`                | string     | 交易標的，例如 `BTC-USD`。                                                                       |
| `data.items.policy.triggerPercent`        | integer    | 相對於開倉價的觸發比例。                                                                             |
| `data.items.policy.triggerPrice`          | string     | 觸發價格。                                                                                    |
| `data.items.triggerEvents.createdAt`      | integer    | 觸發時間戳，毫秒。                                                                                |
| `data.items.triggerEvents.triggerEventId` | string     | 觸發事件唯一識別碼。                                                                               |
| `data.items.triggerEvents.triggerReason`  | string     | 觸發原因，例如 `LIQ_PREVENT`、`INS_TAKE_PROFIT`、`EXPIRED`、`CANCELLED_*`。                         |
| `data.limit`                              | integer    | 每頁筆數。                                                                                    |
| `data.offset`                             | integer    | 分頁偏移。                                                                                    |
| `data.sort`                               | string     | 排序方式。                                                                                    |
| `data.timeAxis`                           | string     | 時間軸欄位。                                                                                   |
| `data.total`                              | integer    | 總筆數。                                                                                     |
| `success`                                 | boolean    | 請求是否成功。                                                                                  |
