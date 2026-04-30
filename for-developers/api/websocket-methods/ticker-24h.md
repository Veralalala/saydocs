---
description: Rolling ~24h ticker from Redis oracle:ticker24h per symbol.
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/websocket-fang-fa/24-xiao-shi-ticker-ding-yue
---

# ticker（24h）

## Subscribe ticker\_24h

Send a **WebSocket text frame** with JSON.&#x20;

### Subscribe request

| Field         | Type      | Required | Description            |
| ------------- | --------- | -------- | ---------------------- |
| `event`       | string    | Yes      | `sub`.                 |
| `topic`       | string    | Yes      | `ticker_24h`.          |
| `symbols`     | string\[] | Yes      | Non-empty symbol list. |
| `compression` | integer   | No       | `0` / `1` outbound.    |
| `id`          | string    | No       | Echoed on pushes.      |

#### Example

```json
{
  "event": "sub",
  "topic": "ticker_24h",
  "symbols": ["BTC-USD", "ETH-USD"]
}
```

### Notification: ticker\_24h push

| Field         | Type    | Required | Description                |
| ------------- | ------- | -------- | -------------------------- |
| `topic`       | string  | Yes      | `ticker_24h`.              |
| `pair`        | string  | Yes      | Symbol for this frame.     |
| `t`           | integer | Yes      | Server send time, Unix ms. |
| `id`          | string  | No       | Echo.                      |
| `compression` | integer | No       | Encoding flag.             |
| `data`        | object  | Yes      | rolling \~24h window.      |

#### Common `data` fields

| Field      | Type    | Description                  |
| ---------- | ------- | ---------------------------- |
| `P`        | string  | Percent-style field          |
| `c`        | string  | Current / close-style value. |
| `o`        | string  | Window open reference.       |
| `q`        | string  | Quote notional / turnover.   |
| `s`        | string  | Symbol.                      |
| `st`, `et` | integer | Window start/end, Unix ms.   |
| `ts_ms`    | integer | Data timestamp, Unix ms.     |

Additional keys may appear per marketdata implementation.

## Unsubscribe ticker\_24h

Send a **WebSocket text frame** with JSON (symmetric to Subscribe ticker\_24h).

### Request

| Field         | Type      | Required | Description        |
| ------------- | --------- | -------- | ------------------ |
| `event`       | string    | Yes      | `unsub`.           |
| `topic`       | string    | Yes      | `ticker_24h`.      |
| `symbols`     | string\[] | Yes      | Symbols to remove. |
| `compression` | integer   | No       | Optional.          |
| `id`          | string    | No       | Optional.          |

#### Example

```json
{
  "event": "unsub",
  "topic": "ticker_24h",
  "symbols": ["BTC-USD"]
}
```

### Response

No dedicated server JSON ack.
