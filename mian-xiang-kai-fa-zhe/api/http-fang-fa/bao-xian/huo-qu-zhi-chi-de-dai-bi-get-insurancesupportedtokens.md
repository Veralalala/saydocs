# 获取支持的代币（GET /insurance/supported-tokens）

查詢目前可投保的市場、支援的保險類型、槓桿範圍與保險時長範圍。

```
GET /v1/public/exchange/insurance/supported-tokens
```

#### 回應

```json
{
  "success": true,
  "minQuoteIsolatedMargin": "10",
  "data": [
    {
      "symbol": "BTC-USD",
      "market": "BTC-USD",
      "insuranceTypes": [
        { "code": "REVIVAL", "type": 1 }
      ],
      "minLeverage": "2",
      "maxLeverage": "50",
      "minDurationHours": 24,
      "maxDurationHours": 168
    }
  ]
}
```
