---
description: 按地址訂閱鏈上帳本廣播
---

# 帳本訂閱

傳送一個 **WebSocket 文字幀**，訊息體為 JSON。

`topic=ledger` ，使用 **`addresses`**，不使用 `symbols`。

### 訂閱請求

<table><thead><tr><th width="157.28125">欄位</th><th width="129.3046875">型別</th><th width="90.921875">必填</th><th>說明</th><th>列舉</th></tr></thead><tbody><tr><td><code>event</code></td><td>string</td><td>是</td><td><code>sub</code>：訂閱；<code>unsub</code>：取消訂閱。其他值會報錯。注意：<code>system</code> 心跳使用獨立 Schema，不要用 <code>topic=system</code> 搭配 <code>sub</code></td><td>列舉：sub,unsub</td></tr><tr><td><code>topic</code></td><td>string</td><td>是</td><td>頻道主題。<code>price</code>：Oracle 價格；<code>ledger</code>：鏈上帳本廣播；<code>kline</code>：K 線；<code>ticker_24h</code>：約 24h 滾動 Ticker；日榜：<code>pct_rank</code>、<code>pct_rank_asc</code>、<code>volume_rank</code>、<code>volume_rank_asc</code>；24h：<code>pct_rank_24h</code>、<code>pct_rank_24h_asc</code>、<code>volume_rank_24h</code>、<code>volume_rank_24h_asc</code></td><td>列舉：price,ledger,kline,ticker_24h,pct_rank,pct_rank_asc,volume_rank,volume_rank_asc,pct_rank_24h,pct_rank_24h_asc,volume_rank_24h,volume_rank_24h_asc</td></tr><tr><td><code>addresses</code></td><td>string[]</td><td>否</td><td><code>topic=ledger</code> 時必填</td><td></td></tr><tr><td><code>compression</code></td><td>integer</td><td>否</td><td>可選。出站推送是否壓縮：<code>0</code> 普通 UTF-8 JSON 文字；<code>1</code> 先 gzip 再 Latin-1 映射為<strong>文字幀</strong>（仍為 text frame）。非法值（非 0/1）回傳 <code>WS_BAD_REQUEST</code>。</td><td>列舉：0,1</td></tr><tr><td><code>id</code></td><td>string</td><td>否</td><td>客戶端請求 ID。若設定，會在推送中原樣回顯。</td><td></td></tr><tr><td><code>interval</code></td><td>string</td><td>否</td><td><strong>僅 <code>topic=kline</code> 必填</strong>。K 線週期，小寫，與 Redis <code>oracle:kline:rt:{SYMBOL}:{interval}</code> 及 MQ fanout 週期一致</td><td>列舉：1m,5m,15m,1h,4h,1d,1w</td></tr><tr><td><code>limit</code></td><td>integer</td><td>否</td><td><strong>僅排行類 topic 使用</strong>。請求的回傳行數；<code>0</code>/省略表示使用伺服器預設 <code>rank_top_n</code></td><td>最小值：0</td></tr><tr><td><code>symbols</code></td><td>string []</td><td>否</td><td>交易對列表。<code>price</code>/<code>kline</code>/<code>ticker_24h</code>：必填且須包含有效 symbol（正規化後字元集為 A-Z、0-9、<code>.</code>、<code>-</code>、<code>_</code>）。排行類 topic：須省略、空陣列或僅 <code>["*"]</code>。<strong><code>topic=ledger</code> 時不要使用</strong>（改用 <code>addresses</code>）。</td><td></td></tr></tbody></table>

#### 範例

```json
{
  "event": "sub",
  "topic": "ledger",
  "addresses": ["YourSolanaAddressHere..."]
}
```

### 推送訊息：帳本事件

這個主題**沒有頂層 `pair` 欄位**。請根據 `data` 內部欄位識別具體流水。

| 欄位            | 型別      | 必填 | 說明               |
| ------------- | ------- | -- | ---------------- |
| `topic`       | string  | 是  | 固定為 `ledger`。    |
| `t`           | integer | 是  | 伺服器傳送時間，Unix 毫秒。 |
| `id`          | string  | 否  | 請求 ID 回顯。        |
| `compression` | integer | 否  | 編碼標記。            |
| `data`        | object  | 是  | 帳本事件物件。          |

## 取消訂閱帳本

傳送一個 **WebSocket 文字幀**，訊息體為 JSON。

### 請求

| 欄位            | 型別        | 必填 | 說明            |
| ------------- | --------- | -- | ------------- |
| `event`       | string    | 是  | 固定為 `unsub`。  |
| `topic`       | string    | 是  | 固定為 `ledger`。 |
| `addresses`   | string\[] | 是  | 要移除的地址列表。     |
| `compression` | integer   | 否  | 可選。           |
| `id`          | string    | 否  | 可選。           |

`ledger` 主題不要傳 `symbols`。

#### 範例

```json
{
  "event": "unsub",
  "topic": "ledger",
  "addresses": ["YourSolanaAddressHere..."]
}
```

### 回應

正式環境通常不會回傳專門的 JSON 確認幀。OpenAPI 中可能只會顯示 `_doc` 佔位物件。
