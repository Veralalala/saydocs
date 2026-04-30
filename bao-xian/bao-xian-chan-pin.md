---
description: 本頁說明目前已實作的險種代碼、參數含義與組合規則。
---

# 保險產品

### 兩類產品

| 名稱（文件用語）               | 作用概要                                                                                              |
| ---------------------- | ------------------------------------------------------------------------------------------------- |
| **保本險**（Zero Loss）     | 倉位到達由 `trigger_percent` 決定的虧損閾值時平倉，並按 `payout_percent` 賠付 `isolatedMargin` 的指定比例（預設 100%）         |
| **利增險**（Double Profit） | 倉位到達由 `trigger_percent` 決定的保證金 ROI 價位時平倉，並按 `payout_percent` 額外賠付 `isolatedMargin` 的指定比例（預設 100%） |

兩者都綁定**逐倉**倉位；在 API / 模型中對應欄位為 `insuranceType`。

***

### 核心參數

* **`trigger_percent`**：
  * 控制**觸發價格 / 觸發閾值**的比例參數
  * 對利增險，表示目標保證金 ROI 檔位，用於按獲利方向計算 `triggerPrice`
  * 對保本險，表示目標保證金虧損檔位，用於按虧損方向計算 `triggerPrice`
* **`triggerPrice`**
  * 保險實際觸發價格，由險種類型和倉位參數決定
  * 利增險：`triggerPrice = entry ± (margin × trigger_percent / 100) / size`
  * 保本險：`triggerPrice = entry ∓ (margin × trigger_percent / 100) / size`
* **`payout_percent`**
  * 只用於控制**賠付比例**
  * 賠付額統一為 `isolatedMargin × payout_percent / 100`
  * exposure 口径也统一按 `payout_percent` 计算

***

### 兩種險可在同一倉位上**同時生效**，互不排斥

* "可同時生效"只表示同一倉位可以同時持有一張 active **保本險**和一張 active **利增險**
* 真正發生觸發時，仍然**只會命中一個觸發原因**
* 原因不是系統做雙觸發競爭，而是任一觸發一旦成立，後續動作都是按**整倉關閉**執行；倉位關閉後，另一險種立即失去可觸發對象

***

### 時長與檔位

* 對外目前僅支援 **24h / 72h / 168h** 等**固定檔位**
* `trigger_percent`
  * **利增險**：10%\~100%
  * **保本險：**&#x31;00%
* `payout_percent`
  * **利增險**：100%
  * **保本險：**&#x31;0%\~100%

***

### 支援市場

* **BTC-USD、ETH-USD** 等，實際以介面或接口查詢結果為準。

***

### 協議

* 新購、續保，或開倉並投保前，需先滿足 [**保險產品協議**](../feng-xian-yu-zheng-ce/bao-xian-chan-pin-xie-yi/) 的版本要求。

***

### 相關頁面

* [保單生命週期](bao-dan-sheng-ming-zhou-qi.md)
* [觸發條件](chu-fa-tiao-jian.md)
