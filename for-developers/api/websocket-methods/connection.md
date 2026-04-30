---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/websocket-fang-fa/lian-xian
---

# Connection

## Connect

### Request

```
GET wss://sayfi1-t.telepath.world/ws
```

### Response

On success the server returns **101 Switching Protocols**. There is **no JSON body** on the HTTP response.

## Disconnect notification

The server may emit one final **text frame** before closing the connection.&#x20;

### Notification payload

| Field     | Type    | Required | Description                 |
| --------- | ------- | -------- | --------------------------- |
| `topic`   | string  | Yes      | `disconnect`.               |
| `code`    | string  | Yes      | Machine-readable reason.    |
| `message` | string  | Yes      | Human-readable explanation. |
| `t`       | integer | Yes      | Server timestamp, Unix ms.  |

### Common `code` values

| Code                    | Meaning                                           |
| ----------------------- | ------------------------------------------------- |
| `SERVER_SHUTDOWN`       | Graceful shutdown.                                |
| `APP_HEARTBEAT_TIMEOUT` | Application `system`/`ping` not received in time. |
| `READ_IDLE_TIMEOUT`     | Read idle / protocol timeout.                     |
| `OUTBOUND_QUEUE_FULL`   | Outbound queue saturated.                         |

## Error notification

### Payload

| Field     | Type   | Required | Description                                                             |
| --------- | ------ | -------- | ----------------------------------------------------------------------- |
| `code`    | string | Yes      | Error class.                                                            |
| `message` | string | Yes      | Short reason (often English), e.g. `invalid symbol`, `missing symbols`. |

### `code` values

| Code              | Meaning                                                                                                                                       |
| ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| `WS_INVALID_JSON` | Frame is not valid JSON.                                                                                                                      |
| `WS_BAD_REQUEST`  | Bad fields, missing `symbols`, illegal `interval`, rank topic symbol rules, invalid `compression`, unsupported `topic`, etc. — see `message`. |

### Example

```json
{
  "code": "WS_BAD_REQUEST",
  "message": "missing symbols"
}
```
