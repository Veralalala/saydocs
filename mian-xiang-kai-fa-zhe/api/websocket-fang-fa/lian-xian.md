# 連線

### 請求

```
GET wss://sayfi1-t.telepath.world/ws
```

### 回應

握手成功時，伺服器回傳 **101 Switching Protocols**。HTTP 回應本身**沒有 JSON 回應體**。

## 斷線通知

伺服器在關閉連線前，可能會額外傳送最後一個 **文字幀**。

### 通知結構

| 欄位        | 型別      | 必填 | 說明                |
| --------- | ------- | -- | ----------------- |
| `topic`   | string  | 是  | 固定為 `disconnect`。 |
| `code`    | string  | 是  | 機器可讀的斷線原因。        |
| `message` | string  | 是  | 面向使用者的簡短說明。       |
| `t`       | integer | 是  | 伺服器時間戳，Unix 毫秒。   |

### 常見 `code` 值

| 代碼                      | 含義                              |
| ----------------------- | ------------------------------- |
| `SERVER_SHUTDOWN`       | 伺服器正常下線。                        |
| `APP_HEARTBEAT_TIMEOUT` | 在規定時間內未收到應用層 `system` / `ping`。 |
| `READ_IDLE_TIMEOUT`     | 讀取閒置逾時或協議逾時。                    |
| `OUTBOUND_QUEUE_FULL`   | 出站訊息佇列已滿。                       |

## 錯誤通知

### 結構

| 欄位        | 型別     | 必填 | 說明                                        |
| --------- | ------ | -- | ----------------------------------------- |
| `code`    | string | 是  | 錯誤類別。                                     |
| `message` | string | 是  | 簡短原因說明，通常直接使用伺服器錯誤文案，例如 `invalid symbol`。 |

### `code` 值

| 代碼                | 含義                                                                                               |
| ----------------- | ------------------------------------------------------------------------------------------------ |
| `WS_INVALID_JSON` | 文字幀不是合法 JSON。                                                                                    |
| `WS_BAD_REQUEST`  | 欄位錯誤、缺少 `symbols`、`interval` 非法、排行主題的 symbol 規則錯誤、`compression` 非法、`topic` 不支援等。具體原因見 `message`。 |

### 範例

```json
{
  "code": "WS_BAD_REQUEST",
  "message": "missing symbols"
}
```
