---
description: >-
  Subscribe to K-line topic with interval; first push is snapshot data array,
  then realtime bars.
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/websocket-fang-fa/k-xian-ding-yue
---

# kline

## Subscribe kline

### Subscribe request

<table><thead><tr><th width="133.2265625">Field</th><th width="102.25390625">Type</th><th width="113.46484375">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>event</code></td><td>string</td><td>Yes</td><td><code>sub</code>.</td></tr><tr><td><code>topic</code></td><td>string</td><td>Yes</td><td><code>kline</code>.</td></tr><tr><td><code>symbols</code></td><td>string[]</td><td>Yes</td><td>Non-empty symbol list.</td></tr><tr><td><code>interval</code></td><td>string</td><td>Yes</td><td><code>1m</code>, <code>5m</code>, <code>15m</code>, <code>1h</code>, or <code>1d</code> </td></tr><tr><td><code>compression</code></td><td>integer</td><td>No</td><td><p>Optional. Outbound push compression: <code>0</code> Normal UTF-8 JSON text; <code>1</code> First gzip, then Latin-1 mapped to a <strong>text frame</strong> (still a text frame).</p><p>Illegal values ​​(not 0/1) return <code>WS_BAD_REQUEST</code>.</p></td></tr><tr><td><code>id</code></td><td>string</td><td>No</td><td>Optional. Client-side custom request associated ID. Server-side <strong>returns the original content</strong> in the corresponding topic's push notifications (if provided), facilitating front-end matching of subscriptions and push notifications.</td></tr></tbody></table>

#### Example

```json
{
  "event": "sub",
  "topic": "kline",
  "symbols": ["BTC-USD"],
  "interval": "5m",
  "id": "k-1"
}
```

### Notification: snapshot

First push after subscribe uses **`data` as an array** of bars (max **300** elements). Top-level fields:

| Field         | Type      | Required | Description                          |
| ------------- | --------- | -------- | ------------------------------------ |
| `topic`       | string    | Yes      | `kline`.                             |
| `pair`        | string    | Yes      | Symbol.                              |
| `interval`    | string    | Yes      | Same as subscription.                |
| `t`           | integer   | Yes      | Server send time, Unix ms.           |
| `id`          | string    | No       | Echo.                                |
| `compression` | integer   | No       | `0` or `1`.                          |
| `data`        | object\[] | Yes      | List of `WsKlineBar`-shaped objects. |

#### Snapshot bar (`data[]` element)

| Field         | Type    | Description                                     |
| ------------- | ------- | ----------------------------------------------- |
| `c`           | string  | Close .                                         |
| `o`, `h`, `l` | string  | Open / high / low.                              |
| `st`, `et`    | integer | Bucket start/end, Unix ms; interval `[st, et)`. |
| `interval`    | string  | e.g. `5m`.                                      |
| `s`           | string  | Symbol.                                         |
| `pct`         | string  | Derived change                                  |
| `written_ms`  | integer | Generation time for debugging.                  |

### Notification: realtime

After the snapshot, realtime updates use a **single object** in `data`. See Kline realtime notification.



## Unsubscribe kline

Send a **WebSocket text frame** with JSON.

Unsubscribe kline with the same `symbols` and `interval`.

### Request

| Field         | Type      | Required | Description                                             |
| ------------- | --------- | -------- | ------------------------------------------------------- |
| `event`       | string    | Yes      | `unsub`.                                                |
| `topic`       | string    | Yes      | `kline`.                                                |
| `symbols`     | string\[] | Yes      | Symbols to stop.                                        |
| `interval`    | string    | Yes      | Same interval as the active subscription (`1m` … `1d`). |
| `compression` | integer   | No       | Optional; often omitted for `unsub`.                    |
| `id`          | string    | No       | Optional.                                               |

#### Example

```json
{
  "event": "unsub",
  "topic": "kline",
  "symbols": ["BTC-USD"],
  "interval": "5m"
}
```

### Response

No dedicated server JSON ack; doc may show `_doc` placeholders only.

## Kline realtime notification

After Subscribe kline delivers the **snapshot** (`data` array), MQ fanout produces **realtime** frames where `data` is **one** bar object (same shape as each snapshot element).

### Notification payload

| Field         | Type    | Required | Description                                    |
| ------------- | ------- | -------- | ---------------------------------------------- |
| `topic`       | string  | Yes      | `kline`.                                       |
| `pair`        | string  | Yes      | Symbol.                                        |
| `interval`    | string  | Yes      | Matches subscription and bar.                  |
| `t`           | integer | Yes      | Server send time, Unix ms.                     |
| `id`          | string  | No       | Subscription id echo.                          |
| `compression` | integer | No       | `0` plain; `1` gzip + Latin-1 text.            |
| `data`        | object  | Yes      | Single bar; fields follow upstream / PROTOCOL. |

### `data` object (typical fields)

| Field         | Type    | Description                         |
| ------------- | ------- | ----------------------------------- |
| `c`           | string  | Close.                              |
| `o`, `h`, `l` | string  | OHLC strings.                       |
| `st`, `et`    | integer | Bucket bounds, Unix ms; `[st, et)`. |
| `interval`    | string  | Period, e.g. `5m`.                  |
| `s`           | string  | Symbol.                             |
| `pct`         | string  | Derived field.                      |
| `written_ms`  | integer | Write timestamp for ops.            |

Exact fields may vary slightly by upstream; treat as `WsKlineBar`-compatible.
