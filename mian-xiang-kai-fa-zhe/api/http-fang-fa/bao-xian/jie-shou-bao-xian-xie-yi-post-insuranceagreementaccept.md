# 接受保險協議（POST /insurance/agreement/accept）

```
POST /v1/private/insurance/agreement/accept
```

不需要請求體。

#### 回應

```json
{
  "success": true,
  "data": {
    "isAccepted": true,
    "acceptedVersion": 1,
    "acceptedAt": 1700000000000,
    "requiredVersion": 1
  }
}
```
