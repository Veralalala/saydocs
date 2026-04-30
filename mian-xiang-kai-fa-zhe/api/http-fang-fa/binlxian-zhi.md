# 頻率限制

| 層級         | 作用範圍                                | 觸發時機                                                                      | 典型用途                     |
| ---------- | ----------------------------------- | ------------------------------------------------------------------------- | ------------------------ |
| **IP**     | 客戶端 IP（`gin.ClientIP()`）            | 在公共監聽器上，所有 `/v{version}/private/...` 與 `/v{version}/public/...` 請求到達代理時執行 | 第一層防護。在 EIP-712 或上游邏輯前削峰 |
| **地址**     | EIP-712 請求標頭中的錢包地址（`X-Address`，轉小寫） | 僅私有路由。在 `AuthService` 內，**黑名單檢查之後**、**簽名校驗之前** 執行                         | 限制單一簽名地址的吞吐              |
| **重複請求保護** | 私有請求指紋                              | 僅私有路由。在 **EIP-712 校驗成功之後** 執行                                             | 在短時間視窗內攔截相同簽名請求的重放       |

***

### 限制在哪一層執行

在 **public** HTTP 服務上：

1. **私有路由**（`/v{n}/private/...`）\
   **IP 限流** → **EIP-712 中介層**
2. **公開路由**（`/v{n}/public/...`）\
   只執行 **IP 限流**

***

### 用戶端可見回應

#### IP 頻率限制（或缺少 IP）

返回 HTTP **429 Too Many Requests**。回應體欄位為 `success` / `code` / `message`：

| 欄位        | 值                         |
| --------- | ------------------------- |
| `code`    | `GATEWAY_IP_RATE_LIMITED` |
| `message` | `too many requests`       |

如果 `ClientIP()` 去除空白後仍為空，也會返回相同結果，因為 Gateway 無法將請求歸入特定限流桶。

#### IP 限流階段 Redis 異常

返回 HTTP **503 Service Unavailable**：

| 欄位        | 值                                |
| --------- | -------------------------------- |
| `code`    | `GATEWAY_DEPENDENCY_UNAVAILABLE` |
| `message` | `service unavailable`            |

#### 地址頻率限制（EIP-712 路徑）

返回 HTTP **429 Too Many Requests**：

| 欄位        | 值                   |
| --------- | ------------------- |
| `code`    | `AUTH_RATE_LIMITED` |
| `message` | `too many requests` |

`message` 的實際值來自 `internal/gateway/middleware.go` 中的 `genericMessage`。這是內部實作細節，不會額外暴露。

#### 重複請求（視窗期內）

返回 HTTP **429 Too Many Requests**：

| 欄位        | 值                        |
| --------- | ------------------------ |
| `code`    | `AUTH_DUPLICATE_REQUEST` |
| `message` | `duplicate request`      |
