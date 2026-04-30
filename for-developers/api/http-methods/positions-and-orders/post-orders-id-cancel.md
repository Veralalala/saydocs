---
description: Cancel order.
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/ding-dan-yu-cang-wei/qu-xiao-ding-dan-post-ordersidcancel
---

# POST orders/{id}/cancel

```
POST /v1/private/exchange/orders/{id}/cancel
```

#### Path Parameters

| Parameter | Required | Description |
| --------- | -------- | ----------- |
| `id`      | Yes      | Order id    |

#### Response

```json
{
  "success": true,
  "data": {
    "status": "..."
  }
}
```

#### Response Fields

| Field         | Type    | Description |
| ------------- | ------- | ----------- |
| `data`        | object  |             |
| `data.status` | string  |             |
| `success`     | boolean |             |
