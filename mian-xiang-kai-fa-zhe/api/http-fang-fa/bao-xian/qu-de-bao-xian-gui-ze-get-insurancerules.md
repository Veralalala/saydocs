# 取得保險規則（GET /insurance/rules）

查詢目前生效中的全域保險規則。

```
GET /v1/public/insurance/rules
```

#### 回應

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
