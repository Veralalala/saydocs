# 價格訂閱

傳送一個 **WebSocket 文字幀**，訊息體為 JSON。O

訂閱後**不會單獨回傳確認幀**。第一條 `price` 推送可能是 Redis 快照，之後才進入即時更新。

### 訂閱請求

| 欄位            | 型別        | 必填 | 說明                                                                                                                           |
| ------------- | --------- | -- | ---------------------------------------------------------------------------------------------------------------------------- |
| `event`       | string    | 是  | 固定為 `sub`。                                                                                                                   |
| `topic`       | string    | 是  | 固定為 `price`。                                                                                                                 |
| `symbols`     | string\[] | 否  | 交易對列表。`price`/`kline`/`ticker_24h`/`ticker_multi`：必填且須包含有效 symbol（正規化後字元集為 A-Z、0-9、`.`、`-`、`_`）。排行類 topic：須省略、空陣列或僅 `["*"]`。 |
| `compression` | integer   | 否  | 可選。出站推送是否壓縮：`0`：普通 UTF-8 JSON 文字；`1`：先 gzip 再 Latin-1 映射為**文字幀**（仍為 text frame）。非法值（非 0/1）回傳 `WS_BAD_REQUEST`。               |
| `id`          | string    | 否  | 客戶端請求 ID。若設定，會在推送中回顯。                                                                                                        |
| `interval`    | string    | 否  | **僅 `topic=kline` 必填**。K 線週期，小寫，列舉：1m,5m,15m,1h,4h,1d,1w                                                                     |
| `limit`       | integer   | 否  | **僅排行類 topic 使用**。請求的回傳行數；`0`/省略表示使用伺服器預設 `rank_top_n`。最小值：0                                                                 |

#### 範例

```json
{
  "event": "sub",
  "topic": "price",
  "symbols": ["BTC-USD"],
  "compression": 0,
  "id": "req-1"
}
```

### 推送訊息：價格更新

下行訊息的 **`topic` 固定為 `price`**。這個主題**沒有頂層 `pair` 欄位**，請使用 `data.symbol` 判斷交易對。

| 欄位            | 型別      | 必填 | 說明               |
| ------------- | ------- | -- | ---------------- |
| `topic`       | string  | 是  | 固定為 `price`。     |
| `t`           | integer | 是  | 伺服器傳送時間，Unix 毫秒。 |
| `id`          | string  | 否  | 請求 ID 回顯。        |
| `compression` | integer | 否  | 壓縮標記，`0` 或 `1`。  |
| `data`        | object  | 是  | 價格物件。            |

#### `data` 欄位

| 欄位       | 型別      | 說明                                                         |
| -------- | ------- | ---------------------------------------------------------- |
| `last`   | string  | 最新成交價。優先使用 Oracle 的 `last`，否則回退到 `execution`，再回退到 `index`。 |
| `mark`   | string  | 標記價格。                                                      |
| `symbol` | string  | 正規化後的交易對。                                                  |
| `ts_ms`  | integer | 資料時間戳。                                                     |

## 取消訂閱價格

傳送一個 **WebSocket 文字幀**，訊息體為 JSON。OpenAPI 中通常會用 `POST /_doc/ws/text-frame/unsubscribe-price` 作為佔位說明。

### 請求

| 欄位            | 型別        | 必填 | 說明                      |
| ------------- | --------- | -- | ----------------------- |
| `event`       | string    | 是  | 固定為 `unsub`。            |
| `topic`       | string    | 是  | 固定為 `price`。            |
| `symbols`     | string\[] | 是  | 要移除的交易對列表，正規化規則與訂閱時相同。  |
| `compression` | integer   | 否  | 多數部署會忽略這個欄位。建議省略或傳 `0`。 |
| `id`          | string    | 否  | 可選的請求 ID。               |

#### 範例

```json
{
  "event": "unsub",
  "topic": "price",
  "symbols": ["BTC-USD"]
}
```

### 回應

`unsub` 通常不會回傳專門的 JSON 確認幀。部分 OpenAPI 文件中的 `_doc: true` 只是佔位物件，不是實際伺服器訊息。
