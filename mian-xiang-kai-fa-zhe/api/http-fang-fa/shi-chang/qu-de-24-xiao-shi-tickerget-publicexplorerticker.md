# 取得 24 小時 Ticker（GET /public/explorer/ticker）

```
GET /v1/public/marketdata/ticker
```

#### 查詢參數

| 參數         | 必填 | 說明                                       |
| ---------- | -- | ---------------------------------------- |
| `sort`     | 否  | 例如 `volume_*`，按報價成交額 `q` 排序，與排行 ZSET 一致。 |
| `category` | 否  | `all` 或資料庫欄位 `instrument_type` 對應的分類值。   |
| `limit`    | 否  | 每頁返回數量。                                  |
| `cursor`   | 否  | 上一次回應返回的 `next_cursor`。                  |

#### 回應

```json
{
  "success": true,
  "data": {}
}
```

#### 回應欄位

| 欄位                 | 類型         | 說明                                                |
| ------------------ | ---------- | ------------------------------------------------- |
| `category`         | string     | 與請求參數 `category` 一致，對應資料庫中的 `instrument_type` 過濾。 |
| `count`            | integer    | 目前頁面的返回筆數。                                        |
| `items`            | object \[] | Ticker 列表。                                        |
| `items.rank_score` | number     | 目前排序對應的 ZSET 分值。漲跌幅排序時表示百分比變化，成交額排序時表示報價成交額。      |
| `items.symbol`     | string     | 交易對符號。                                            |
| `items.ticker`     | object     | Redis `oracle:ticker24h` 的 JSON 資料。缺失時可省略。        |
| `limit`            | integer    | 本次請求使用的分頁大小。                                      |
| `next_cursor`      | string     | 下一頁游標。空字串表示沒有更多資料。                                |
| `sort`             | string     | 本次請求使用的排序方式。                                      |
