# K 線訂閱

### 訂閱請求

<table><thead><tr><th width="101.40625">欄位</th><th width="106.953125">型別</th><th width="121.21484375">必填</th><th>說明</th></tr></thead><tbody><tr><td><code>event</code></td><td>string</td><td>是</td><td><code>sub</code>：訂閱；<code>unsub</code>：取消訂閱。其他值會報錯。注意：<code>system</code> 心跳使用獨立 Schema，不要用 <code>topic=system</code> 搭配 <code>sub</code>。</td></tr><tr><td><code>topic</code></td><td>string</td><td>是</td><td>頻道主題。<code>price</code>：Oracle 價格；<code>kline</code>：K 線；<code>ticker_24h</code>：約 24h 滾動 Ticker；<code>ticker_multi</code>：24h + 5m/1h/4h ；日榜：<code>pct_rank</code>、<code>pct_rank_asc</code>、<code>volume_rank</code>、<code>volume_rank_asc</code>；24h：<code>pct_rank_24h</code>、<code>pct_rank_24h_asc</code>、<code>volume_rank_24h</code>、<code>volume_rank_24h_asc</code>。</td></tr><tr><td><code>symbols</code></td><td>string[]</td><td>是</td><td>交易對列表。<code>price</code>/<code>kline</code>/<code>ticker_24h</code>/<code>ticker_multi</code>：必填且須包含有效 symbol（正規化後字元集為 A-Z、0-9、<code>.</code>、<code>-</code>、<code>_</code>）。排行類 topic：須省略、空陣列或僅 <code>["*"]</code>。</td></tr><tr><td><code>interval</code></td><td>string</td><td>是</td><td>K 線週期，小寫，1m,5m,15m,1h,4h,1d,1w</td></tr><tr><td><code>compression</code></td><td>integer</td><td>否</td><td>可選。出站推送是否壓縮：<code>0</code> 普通 UTF-8 JSON 文字；<code>1</code> 先 gzip 再 Latin-1 映射為<strong>文字幀</strong>（仍為 text frame）。非法值（非 0/1）回傳 <code>WS_BAD_REQUEST</code>。</td></tr><tr><td><code>id</code></td><td>string</td><td>否</td><td>可選。客戶端自訂請求關聯 ID。伺服器在對應 topic 的推送中<strong>原樣回顯</strong>（若提供），便於前端匹配訂閱與推送。</td></tr></tbody></table>

#### 範例

```json
{
  "event": "sub",
  "topic": "kline",
  "symbols": ["BTC-USD"],
  "interval": "5m",
  "id": "k-1"
}
```

### 推送訊息：快照

訂閱後的第一筆推送會使用 **`data` 作為 K 線陣列**，最多 **300** 筆。頂層欄位如下：

| 欄位            | 型別        | 必填 | 說明                    |
| ------------- | --------- | -- | --------------------- |
| `topic`       | string    | 是  | `kline`。              |
| `pair`        | string    | 是  | Symbol。               |
| `interval`    | string    | 是  | 與訂閱請求相同。              |
| `t`           | integer   | 是  | 伺服器傳送時間，Unix 毫秒。      |
| `id`          | string    | 否  | 回顯值。                  |
| `compression` | integer   | 否  | `0` 或 `1`。            |
| `data`        | object\[] | 是  | `WsKlineBar` 形狀的物件列表。 |

#### 快照 K 線（`data[]` 元素）

| 欄位            | 型別      | 說明                                     |
| ------------- | ------- | -------------------------------------- |
| `c`           | string  | 收盤價。                                   |
| `o`, `h`, `l` | string  | 開盤 / 最高 / 最低。                          |
| `st`, `et`    | integer | bucket 開始與結束時間，Unix 毫秒；區間為 `[st, et)`。 |
| `interval`    | string  | 例如 `5m`。                               |
| `s`           | string  | Symbol。                                |
| `pct`         | string  | 衍生變動值。                                 |
| `written_ms`  | integer | 產生時間，可用於除錯。                            |

### 推送訊息：即時更新

快照之後，即時更新會在 `data` 中使用**單一物件**。詳見下方的 K 線即時通知。

## 取消訂閱 K 線

傳送一個 **WebSocket 文字幀**，訊息體為 JSON。

取消訂閱時，請使用與原訂閱相同的 `symbols` 和 `interval`。

### 請求

| 欄位            | 型別        | 必填 | 說明                        |
| ------------- | --------- | -- | ------------------------- |
| `event`       | string    | 是  | `unsub`。                  |
| `topic`       | string    | 是  | `kline`。                  |
| `symbols`     | string\[] | 是  | 要停止的 symbols。             |
| `interval`    | string    | 是  | 與生效中訂閱相同的週期（`1m` … `1d`）。 |
| `compression` | integer   | 否  | 可選；`unsub` 通常會省略。         |
| `id`          | string    | 否  | 可選。                       |

#### 範例

```json
{
  "event": "unsub",
  "topic": "kline",
  "symbols": ["BTC-USD"],
  "interval": "5m"
}
```

### 回應

不會有專門的伺服器 JSON 確認訊息；文件中可能只會顯示 `_doc` 佔位內容。

## K 線即時通知

`Subscribe kline` 傳回**快照**（`data` 陣列）之後，MQ fanout 會產生**即時**幀，此時 `data` 是**單一** K 線物件，形狀與每個快照元素相同。

### 通知內容

| 欄位            | 型別      | 必填 | 說明                                |
| ------------- | ------- | -- | --------------------------------- |
| `topic`       | string  | 是  | `kline`。                          |
| `pair`        | string  | 是  | Symbol。                           |
| `interval`    | string  | 是  | 與訂閱和 K 線資料一致。                     |
| `t`           | integer | 是  | 伺服器傳送時間，Unix 毫秒。                  |
| `id`          | string  | 否  | 訂閱 ID 回顯。                         |
| `compression` | integer | 否  | `0` 為純文字；`1` 為 gzip + Latin-1 文字。 |
| `data`        | object  | 是  | 單一 K 線。                           |

### `data` 物件（常見欄位）

| 欄位            | 型別      | 說明                                |
| ------------- | ------- | --------------------------------- |
| `c`           | string  | 收盤價。                              |
| `o`, `h`, `l` | string  | OHLC 字串。                          |
| `st`, `et`    | integer | bucket 邊界，Unix 毫秒；區間為 `[st, et)`。 |
| `interval`    | string  | 週期，例如 `5m`。                       |
| `s`           | string  | Symbol。                           |
| `pct`         | string  | 衍生欄位。                             |
| `written_ms`  | integer | 寫入時間戳，可用於運維排查。                    |

具體欄位可能因上游略有差異；請按 `WsKlineBar` 相容格式處理。
