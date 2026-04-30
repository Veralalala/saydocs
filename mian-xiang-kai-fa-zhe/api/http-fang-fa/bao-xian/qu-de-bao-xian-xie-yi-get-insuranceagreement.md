# 取得保險協議（GET /insurance/agreement）

查詢目前使用者對保險協議的接受狀態。

```
GET /v1/public/insurance/agreement
```

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

***
