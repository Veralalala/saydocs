---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/websocket-fang-fa
---

# WebSocket Methods

### Client message format

Every **client → server** frame is a single JSON object.

| Field         | Type      | Required            | Description                                                                                                       |
| ------------- | --------- | ------------------- | ----------------------------------------------------------------------------------------------------------------- |
| `event`       | string    | For subscribe flows | `sub`, `unsub`, or for heartbeat `ping` (with `topic: "system"`).                                                 |
| `topic`       | string    | Yes\*               | Channel or control: `price`, `ledger`, `kline`, `ticker_24h`, rank topics, `system` (heartbeat only).             |
| `symbols`     | string\[] | Per topic           | Required for `price` / `kline` / `ticker_24h`. For rank topics use omit, `[]`, or `["*"]`. Not used for `ledger`. |
| `addresses`   | string\[] | For `ledger`        | On-chain addresses (see Subscribe ledger).                                                                        |
| `interval`    | string    | For `kline`         | One of `1m`, `5m`, `15m`, `1h`, `1d`.                                                                             |
| `compression` | integer   | No                  | Outbound encoding: `0` plain JSON, `1` gzip then Latin-1 text frame. Invalid → `WS_BAD_REQUEST`.                  |
| `id`          | string    | No                  | Client id echoed on matching pushes when provided.                                                                |

Do not combine `topic: "system"` with `event: "sub"`.

### Server message format

**Server → client** frames are one JSON object per text frame. After a successful subscribe, data arrives as pushes keyed by `topic`. Some frames are control-only (`system`, `disconnect`) or errors (no `topic` in the same way — see Error notification).

| Field         | Type            | Description                                                                      |
| ------------- | --------------- | -------------------------------------------------------------------------------- |
| `topic`       | string          | Push channel or `system` / `disconnect`.                                         |
| `t`           | integer         | Server Unix timestamp in milliseconds (where applicable).                        |
| `id`          | string          | Echo of subscription `id` when the client sent one.                              |
| `compression` | integer         | `0` or `1` — same semantics as client `compression` for this frame.              |
| `pair`        | string          | Present on many pushes; **omitted** on `price` and `ledger` (use `data.symbol`). |
| `data`        | object or array | Payload; shape depends on `topic`.                                               |

If `compression` is `1`, decompress before parsing JSON (gzip, then interpret as text).

### Method reference

#### Connection

| Page                               | Description                                                  |
| ---------------------------------- | ------------------------------------------------------------ |
| [Connect (GET /ws)](connection.md) | Handshake, optional auth headers, `101 Switching Protocols`. |

#### Market streams

| Page                                    | Description                                         |
| --------------------------------------- | --------------------------------------------------- |
| [Subscribe price](price.md)             | Oracle `price` stream; snapshot + realtime.         |
| [Subscribe kline](rank-24h.md)          | K-line subscription; snapshot array then realtime.  |
| [Kline realtime notification](kline.md) | Single-bar `data` object after snapshot.            |
| [Subscribe ticker\_24h](ticker-24h.md)  | Rolling \~24h ticker from Redis `oracle:ticker24h`. |
| [Subscribe ledger](ledger.md)           | On-chain ledger events by `addresses`.              |
| [Subscribe rank (daily)](rank-daily.md) | `pct_rank`, `volume_rank` full tables.              |
| [Subscribe rank (24h)](rank-24h.md)     | `pct_rank_24h`, `volume_rank_24h` full tables.      |
