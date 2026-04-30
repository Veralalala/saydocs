---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/bao-xian/qu-de-bao-xian-xie-yi-get-insuranceagreement
---

# GET insurance/agreement

Query the current user's insurance agreement acceptance status.

```
GET /v1/public/insurance/agreement
```

#### Response

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
