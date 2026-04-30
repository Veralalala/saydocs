---
description: >-
  Subscribe to on-chain ledger broadcasts by addresses (topic ledger); uses
  addresses not symbols.
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/websocket-fang-fa/zhang-ben-ding-yue
---

# ledger

## Subscribe ledger

Send a **WebSocket text frame** with JSON.&#x20;

`topic=ledger` ，uses **`addresses`**, not `symbols`. Do not send `symbols` for this topic.

### Subscribe request

| Field         | Type      | Required | Description                                                                            |
| ------------- | --------- | -------- | -------------------------------------------------------------------------------------- |
| `event`       | string    | Yes      | `sub`.                                                                                 |
| `topic`       | string    | Yes      | `ledger`.                                                                              |
| `addresses`   | string\[] | No       | Non-empty chain addresses (length 4–128); trimmed; matched to `wallet_address` / `to`. |
| `compression` | integer   | No       | `0` / `1` outbound.                                                                    |
| `id`          | string    | No       | Echoed on pushes.                                                                      |

#### Example

```json
{
  "event": "sub",
  "topic": "ledger",
  "addresses": ["YourSolanaAddressHere..."]
}
```

### Notification: ledger push

**No top-level `pair`** — identify flow via fields inside `data`.

| Field         | Type    | Required | Description                                                                                                                    |
| ------------- | ------- | -------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `topic`       | string  | Yes      | `ledger`.                                                                                                                      |
| `t`           | integer | Yes      | Server send time, Unix ms.                                                                                                     |
| `id`          | string  | No       | Echo.                                                                                                                          |
| `compression` | integer | No       | Encoding flag.                                                                                                                 |
| `data`        | object  | Yes      | Ledger event (server may strip `tx_id`; `entries` filtered to `account_kind` prefix `USER`, without `line_no` / `account_id`). |

## Unsubscribe ledger

Send a **WebSocket text frame** with JSON.&#x20;

### Request

| Field         | Type      | Required | Description                            |
| ------------- | --------- | -------- | -------------------------------------- |
| `event`       | string    | Yes      | `unsub`.                               |
| `topic`       | string    | Yes      | `ledger`.                              |
| `addresses`   | string\[] | Yes      | Addresses to remove from subscription. |
| `compression` | integer   | No       | Optional.                              |
| `id`          | string    | No       | Optional.                              |

Do not use `symbols` for `ledger`.

#### Example

```json
{
  "event": "unsub",
  "topic": "ledger",
  "addresses": ["YourSolanaAddressHere..."]
}
```

### Response

No dedicated JSON ack frame in production; OpenAPI may use `_doc` placeholders.

