---
description: >-
  Subscribe to Oracle price pushes (topic price, event sub); optional
  compression and client id.
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/websocket-fang-fa/jia-ge-ding-yue
---

# price

## Subscribe price

Send a **WebSocket text frame** whose body is JSON (not HTTP).&#x20;

There is **no separate sub-ack frame**; the first `price` push may be a Redis snapshot, then realtime updates.

### Subscribe request

| Field         | Type      | Required | Description                                                  |
| ------------- | --------- | -------- | ------------------------------------------------------------ |
| `event`       | string    | Yes      | `sub`.                                                       |
| `topic`       | string    | Yes      | `price`.                                                     |
| `symbols`     | string\[] | Yes      | Non-empty; symbols normalized (`A–Z`, `0–9`, `.`, `-`, `_`). |
| `compression` | integer   | No       | `0` or `1` for outbound pushes.                              |
| `id`          | string    | No       | Echoed on pushes when set.                                   |

#### Example

```json
{
  "event": "sub",
  "topic": "price",
  "symbols": ["BTC-USD"],
  "compression": 0,
  "id": "req-1"
}
```

### Notification: price push

Downlink frames use **`topic`: `price`**. Protocol note: **`price` omits top-level `pair`**; use `data.symbol`.

| Field         | Type    | Required | Description                |
| ------------- | ------- | -------- | -------------------------- |
| `topic`       | string  | Yes      | `price`.                   |
| `t`           | integer | Yes      | Server send time, Unix ms. |
| `id`          | string  | No       | Subscription id echo.      |
| `compression` | integer | No       | `0` or `1`.                |
| `data`        | object  | Yes      | Price object.              |

#### `data` fields

| Field    | Type    | Description                                           |
| -------- | ------- | ----------------------------------------------------- |
| `last`   | string  | Prefer Oracle `last`; else `execution`, then `index`. |
| `mark`   | string  | Prefer Oracle `mark`; else `execution`.               |
| `symbol` | string  | Normalized symbol.                                    |
| `ts_ms`  | integer | Oracle time when present; else filled by service.     |

## Unsubscribe price

Send a **WebSocket text frame** with JSON body. Doc placeholder: `POST /_doc/ws/text-frame/unsubscribe-price`.

### Request

| Field         | Type      | Required | Description                                          |
| ------------- | --------- | -------- | ---------------------------------------------------- |
| `event`       | string    | Yes      | `unsub`.                                             |
| `topic`       | string    | Yes      | `price`.                                             |
| `symbols`     | string\[] | Yes      | Symbols to remove (same normalization as subscribe). |
| `compression` | integer   | No       | Ignored for unsub in most deployments; omit or `0`.  |
| `id`          | string    | No       | Optional correlation id.                             |

#### Example

```json
{
  "event": "unsub",
  "topic": "price",
  "symbols": ["BTC-USD"]
}
```

### Response

There is no dedicated JSON ack frame for `unsub`.&#x20;
