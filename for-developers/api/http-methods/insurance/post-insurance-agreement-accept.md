---
description: >-
  Record the current user's acceptance of the insurance agreement. This is a
  prerequisite for buy, renew
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/bao-xian/jie-shou-bao-xian-xie-yi-post-insuranceagreementaccept
---

# POST insurance/agreement/accept

```
POST /v1/private/insurance/agreement/accept
```

No request body required.

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
