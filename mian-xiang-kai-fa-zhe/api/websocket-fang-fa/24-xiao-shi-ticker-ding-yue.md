# 24 小時 Ticker 訂閱

傳送一個 **WebSocket 文字幀**，訊息體為 JSON。

### 訂閱請求

<table><thead><tr><th width="127.171875">欄位</th><th width="142.625">型別</th><th width="131.69140625">必填</th><th>說明</th></tr></thead><tbody><tr><td><code>event</code></td><td>string</td><td>是</td><td>固定為 <code>sub</code>。</td></tr><tr><td><code>topic</code></td><td>string</td><td>是</td><td>固定為 <code>ticker_24h</code>。</td></tr><tr><td><code>symbols</code></td><td>string[]</td><td>否</td><td>交易對列表。<code>price</code>/<code>kline</code>/<code>ticker_24h</code>/<code>ticker_multi</code>：必填且須包含有效 symbol（正規化後字元集為 A-Z、0-9、<code>.</code>、<code>-</code>、<code>_</code>）。排行類 topic：須省略、空陣列或僅 <code>["*"]</code>。</td></tr><tr><td><code>compression</code></td><td>integer</td><td>否</td><td>可選。出站推送是否壓縮：<code>0</code>：普通 UTF-8 JSON 文字；<code>1</code>：先 gzip 再 Latin-1 映射為<strong>文字幀</strong>（仍為 text frame）。非法值（非 0/1）回傳 <code>WS_BAD_REQUEST</code>。</td></tr><tr><td><code>id</code></td><td>string</td><td>否</td><td>可選。客戶端自訂請求關聯 ID。伺服器在對應 topic 的推送中<strong>原樣回顯</strong>（若提供），便於前端匹配訂閱與推送。</td></tr></tbody></table>

#### 範例

```json
{
  "event": "sub",
  "topic": "ticker_24h",
  "symbols": ["BTC-USD", "ETH-USD"]
}
```

### 推送訊息：ticker\_24h 更新

| 欄位            | 型別      | 必填 | 說明                |
| ------------- | ------- | -- | ----------------- |
| `topic`       | string  | 是  | 固定為 `ticker_24h`。 |
| `pair`        | string  | 是  | 目前幀對應的交易對。        |
| `t`           | integer | 是  | 伺服器傳送時間，Unix 毫秒。  |
| `id`          | string  | 否  | 請求 ID 回顯。         |
| `compression` | integer | 否  | 編碼標記。             |
| `data`        | object  | 是  | 對應滾動約 24 小時視窗。    |

#### 常見 `data` 欄位

| 欄位        | 型別      | 說明                       |
| --------- | ------- | ------------------------ |
| `P`       | string  | 漲跌幅相關欄位。部分協議實作會使用大寫 `P`。 |
| `c`       | string  | 目前值或收盤風格欄位。              |
| `o`       | string  | 視窗起始參考值。                 |
| `q`       | string  | 報價成交額。                   |
| `s`       | string  | 交易對。                     |
| `st`、`et` | integer | 視窗開始和結束時間，Unix 毫秒。       |
| `ts_ms`   | integer | 資料時間戳，Unix 毫秒。           |

不同 marketdata 實作可能會附帶更多欄位。

## 取消訂閱 24 小時 Ticker

傳送一個 **WebSocket 文字幀**，訊息體為 JSON。欄位與訂閱請求對稱。

### 請求

| 欄位            | 型別        | 必填 | 說明                |
| ------------- | --------- | -- | ----------------- |
| `event`       | string    | 是  | 固定為 `unsub`。      |
| `topic`       | string    | 是  | 固定為 `ticker_24h`。 |
| `symbols`     | string\[] | 是  | 要移除的交易對列表。        |
| `compression` | integer   | 否  | 可選。               |
| `id`          | string    | 否  | 可選請求 ID。          |

#### 範例

```json
{
  "event": "unsub",
  "topic": "ticker_24h",
  "symbols": ["BTC-USD"]
}
```

### 回應

通常不會回傳專門的 JSON 確認幀。
