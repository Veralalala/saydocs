---
description: >-
  This page describes the currently supported insurance types, key parameters,
  and combination rules.
metaLinks:
  alternates:
    - https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/bao-xian/bao-xian-chan-pin
---

# Product

### Two product types

| Name              | Code            | Summary                                                                                                                                                                                                                        |
| ----------------- | --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Zero Loss**     | `REVIVAL`       | When price reaches the **loss-side** `triggerPrice` derived from `trigger_percent`, the system closes the position through preventive liquidation logic and pays **`payout_amount`**. This is usually `margin × payout ratio`. |
| **Double Profit** | `PROFIT_DOUBLE` | When price reaches the **profit-side** `triggerPrice` derived from `trigger_percent`, the system closes the position through the insurance take-profit path and pays an additional **`payout_amount`**.                        |

Both products attach to **isolated-margin** positions. In the API and data model, this appears as `insuranceType`.

***

### Core parameters

* **`trigger_percent`** only derives the **trigger price** or risk threshold. Zero Loss calculates `triggerPrice` on the loss side. Double Profit calculates it on the profit side.
* **`payout_percent`** only controls the payout ratio relative to margin. At policy creation, the system fixes it as **`payout_amount = margin × payout_percent / 100`**. It does not change later.

***

### Same-position dual coverage and one trigger per close event

* One position **can** hold one active Zero Loss policy and one active Double Profit policy at the same time. The two types are not mutually exclusive.
* On actual close, a **single close event** can only use one trigger attribution, such as liquidation prevention or insurance take-profit. The other untriggered active policy is **cancelled** and follows the refund flow.

***

### Duration and tiers

* Only fixed terms are supported, such as **24h**, **72h**, and **168h**
* `trigger_percent`: **100%**
* `payout_percent`: **30%**, **50%**, **80%**, **100%**

***

### Supported markets

* **BTC-USD**, **ETH-USD**, and others. The API is the source of truth.

***

### Agreement

* Before buy, renew, or open-and-insure, the user must accept the required version of the [**Insurance Product Agreement**](../risk-and-policy/insurance-product-agreement/).

***

### Related pages

* [**Policy life cycle**](policy-life-cycle.md)
* [**Trigger conditions**](trigger-conditions.md)
