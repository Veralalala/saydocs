---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/binlxian-zhi
---

# Rate limits

| Layer               | Scope                                                         | When it runs                                                                                        | Typical use                                                                               |
| ------------------- | ------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| **IP**              | Client IP (`gin.ClientIP()`)                                  | Public listener: all `/v{version}/private/...` and `/v{version}/public/...` hits the proxy          | First line of defense; damps accidental or abusive bursts before EIP-712 or upstream work |
| **Address**         | Wallet address from EIP-712 headers (`X-Address`, lowercased) | Private routes only, inside `AuthService` **after** blacklist and **before** signature verification | Per-signer throughput cap                                                                 |
| **Duplicate guard** | Fingerprint of private request                                | Private routes only, **after** successful EIP-712 verification                                      | Short window anti-replay for identical signed requests                                    |

***

### Where limits run

On the **public** HTTP server:

1. **Private routes** (`/v{n}/private/...`):\
   **IP limit** → **EIP-712 middleware**
2. **Public routes** (`/v{n}/public/...`):\
   **IP limit** only

***

### Client-visible responses

#### IP rate limit (or missing IP)

HTTP **429 Too Many Requests**, body shape `success` / `code` / `message`:

| Field     | Value                     |
| --------- | ------------------------- |
| `code`    | `GATEWAY_IP_RATE_LIMITED` |
| `message` | `too many requests`       |

If `ClientIP()` is empty after trim, the same response is returned (gateway cannot attribute the request to a bucket).

#### Redis error during IP limit

HTTP **503 Service Unavailable**:

| Field     | Value                            |
| --------- | -------------------------------- |
| `code`    | `GATEWAY_DEPENDENCY_UNAVAILABLE` |
| `message` | `service unavailable`            |

#### Address rate limit (EIP-712 path)

HTTP **429 Too Many Requests**:

| Field     | Value               |
| --------- | ------------------- |
| `code`    | `AUTH_RATE_LIMITED` |
| `message` | `too many requests` |

(Exact `message` comes from `genericMessage` in `internal/gateway/middleware.go`; internal detail is not exposed.)

#### Duplicate request (within window)

HTTP **429 Too Many Requests**:

| Field     | Value                    |
| --------- | ------------------------ |
| `code`    | `AUTH_DUPLICATE_REQUEST` |
| `message` | `duplicate request`      |
