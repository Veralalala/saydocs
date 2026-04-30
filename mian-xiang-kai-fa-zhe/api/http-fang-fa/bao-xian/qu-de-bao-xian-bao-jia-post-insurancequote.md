# 取得保險報價（POST /insurance/quote）

```
POST /v1/public/insurance/quote
```

#### 請求體

| 欄位                 | 型別      | 必填 | 說明                                                                             |
| ------------------ | ------- | -- | ------------------------------------------------------------------------------ |
| `currentMarkPrice` | string  | 否  | 目前標記價格。可省略，由系統使用最新市場資料。                                                        |
| `durationHours`    | integer | 否  | 保險時長，單位為小時。                                                                    |
| `position`         | object  | 是  | 倉位資料。                                                                          |
| `entryPrice`       | string  | 是  | 開倉價格。                                                                          |
| `insuranceType`    | string  | 是  | 保險類型。                                                                          |
| `leverage`         | string  | 是  | 槓桿倍數。                                                                          |
| `liquidationPrice` | string  | 否  | 可選的強平價格。查詢開倉倉位時，`REVIVAL` 可傳入與 `positions.liquidation_price` 一致的值，讓報價與購買路徑更一致。 |
| `margin`           | string  | 是  | 保證金。                                                                           |
| `payoutPercent`    | integer | 否  | 賠付比例。                                                                          |
| `side`             | string  | 是  | 倉位方向。                                                                          |
| `symbol`           | string  | 是  | 交易對。                                                                           |
| `triggerPercent`   | integer | 否  | 觸發比例。                                                                          |

#### 回應

```json
{
  "success": true,
  "data": {
    "quote": {},
    "quotes": []
  }
}
```

#### 回應欄位

| 欄位                                       | 型別         | 說明          |
| ---------------------------------------- | ---------- | ----------- |
| `data`                                   | object     | 回應主體。       |
| `data.quote`                             | object     | 單筆報價。       |
| `data.quote.barrierPrice`                | string     | 障礙價格。       |
| `data.quote.durationHours`               | integer    | 時長。         |
| `data.quote.entryPrice`                  | string     | 開倉價格。       |
| `data.quote.insuranceType`               | integer    | 保險類型。       |
| `data.quote.leverage`                    | string     | 槓桿。         |
| `data.quote.margin`                      | string     | 保證金。        |
| `data.quote.markPriceSnapshot`           | string     | 報價時的標記價格快照。 |
| `data.quote.market`                      | string     | 市場。         |
| `data.quote.notional`                    | string     | 名目價值。       |
| `data.quote.payoutAmount`                | string     | 賠付金額。       |
| `data.quote.payoutPercent`               | integer    | 賠付比例。       |
| `data.quote.positionSize`                | string     | 倉位大小。       |
| `data.quote.premiumPreview`              | object     | 保費預覽。       |
| `data.quote.premiumPreview.totalPremium` | string     | 總保費。        |
| `data.quote.pricedAt`                    | integer    | 報價時間。       |
| `data.quote.side`                        | integer    | 倉位方向。       |
| `data.quote.symbol`                      | string     | 交易對。        |
| `data.quote.triggerPercent`              | integer    | 觸發比例。       |
| `data.quotes`                            | object \[] | 多筆報價列表。     |
| `success`                                | boolean    | 請求是否成功。     |
