---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/bao-xian/qu-de-sheng-xiao-zhong-bao-dan-get-insurancepoliciesactive
---

# GET insurance/policies/active

List only `active` policies for the current user.

```
GET /v1/public/insurance/policies/active
```

#### Query Parameters

| Parameter      | Required | Default | Description                                           |
| -------------- | -------- | ------- | ----------------------------------------------------- |
| `symbol`       | No       | —       | Filter by perpetual symbol, e.g. `BTC-USD`            |
| `limit`        | No       | 20      | Max 200                                               |
| `offset`       | No       | 0       | Pagination offset                                     |
| `expireAtFrom` | No       | —       | Lower bound for `expire_at` (ms timestamp, inclusive) |
| `expireAtTo`   | No       | —       | Upper bound for `expire_at` (ms timestamp, inclusive) |

Results are sorted by `expireAt` ascending (soonest expiry first).

***
