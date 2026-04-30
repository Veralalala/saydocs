---
description: 本頁說明保險退費場景、計算原則與原因枚舉。
---

# 退費規則

### 哪些情況會退費

* **使用者主動退保**（`USER_CANCEL`）。
* **續保 / 替換參數**（`POLICY_REPLACE`）：先對舊單退費，再開新單。`renew` 即 replace 語義。
* **系統強制取消**（`SYSTEM_CANCEL`）等情況。
* **因倉位變化導致保單不再適用**：如使用者**全平**、**非保險 TP / SL** 先觸發，或**強平**但未走保本險賠付路徑等。

> **到期未觸發**（`expired`）**不退**保費。

***

### 狀態路徑

* 預設可退費路徑為：`active` → **`refunding`** → **`cancelled`**。
* 若已過期，或**剩餘公平保費 + 可退風險收益部分 ≤ 0**，也就是極小額或取整後為零，則**不會產生退費事件**。

***

### 計算原則

* **剩餘時間公平保費**：按剩餘時間，結合市場資料與期權方法計算。
* **風險收益部分**：保費中的風險收益部分，會按**剩餘時間**比例退還給使用者。
* **不退的部分**：`fundingFee`、`liqFee` / `closeFee` 等**一次性 / 執行類**成本不退。

> 本文不包含精確公式、分項定義與實作邊界等審計級公式細節。

***

### 退費 `reason` 枚舉

`refund event` 應能區分：

* `USER_CANCEL` — 主動退保
* `POLICY_REPLACE` — 續保 / 調檔替換
* `SYSTEM_CANCEL` — 系統 / 風控 / 協議等強制取消
* `CLOSE` — 使用者平倉，或**一般** TP / SL 導致連帶取消
* `LIQUIDATION` — 清算連帶，或 **REVIVAL 賠付時**伴生取消 **PROFIT\_DOUBLE**
* `TAKE_PROFIT` — **PROFIT\_DOUBLE 賠付時**伴生取消 **REVIVAL**

***

### 續保 / 調檔

* 續保或調檔 = **先退舊單，再開新單**；舊單責任結束，新單重新定價。

***

### 相關頁面

* [保單生命週期](bao-dan-sheng-ming-zhou-qi.md)
* [觸發條件](chu-fa-tiao-jian.md)
* [定價模型](ding-jia-mo-xing.md)
