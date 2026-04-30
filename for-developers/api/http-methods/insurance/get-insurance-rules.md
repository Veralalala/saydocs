---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/bao-xian/qu-de-bao-xian-gui-ze-get-insurancerules
---

# GET insurance/rules

Query the currently active global insurance rules (public endpoint).

```
GET /v1/public/insurance/rules
```

#### Response

```json
{
  "success": true,
  "data": {
    "insuranceTypes": [
      { "code": "REVIVAL", "type": 1 },
      { "code": "PROFIT_DOUBLE", "type": 2 }
    ],
    "supportedDurationHours": [24, 72, 168],
    "payoutPercentOptions": [100],
    "triggerPercentOptions": [80, 90],
    "defaultPayoutPercent": 100,
    "defaultTriggerPercent": 80
  }
}
```
