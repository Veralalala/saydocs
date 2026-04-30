---
description: >-
  This page describes the currently supported insurance types, parameter
  meanings, and combination rules.
---

# Products

### Two product types

| Name              | Code            | Summary                                                                                                                                                                                                                    |
| ----------------- | --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Zero Loss**     | `REVIVAL`       | When the position reaches the loss threshold derived from `trigger_percent`, the system closes the position and pays the configured share of `isolatedMargin` based on `payout_percent`. The default is 100%.              |
| **Double Profit** | `PROFIT_DOUBLE` | When the position reaches the margin ROI target derived from `trigger_percent`, the system closes the position and pays an additional configured share of `isolatedMargin` based on `payout_percent`. The default is 100%. |

Both products attach to **isolated-margin** positions. In the API and data model, this appears as `insuranceType`.

***

### Core parameters

* **`trigger_percent`**
  * This ratio controls the **trigger price** or trigger threshold.
  * For Double Profit, it represents the target margin ROI tier and derives `triggerPrice` on the profit side.
  * For Zero Loss, it represents the target margin loss tier and derives `triggerPrice` on the loss side.
* **`triggerPrice`**
  * This is the actual insurance trigger price. It depends on the product type and position parameters.
  * Double Profit: `triggerPrice = entry ± (margin × trigger_percent / 100) / size`
  * Zero Loss: `triggerPrice = entry ∓ (margin × trigger_percent / 100) / size`
* **`payout_percent`**
  * This only controls the **payout ratio**.
  * The payout amount is always `isolatedMargin × payout_percent / 100`.
  * Exposure uses the same `payout_percent` basis.

***

### Both products can be active on the same position

* A single position can hold one active `REVIVAL` policy and one active `PROFIT_DOUBLE` policy at the same time.
* On actual trigger, only **one trigger reason** can apply.
* This is not a dual-trigger race. Once either trigger is met, the system closes the **entire position**. After the position closes, the other product no longer has a valid trigger target.

***

### Duration and tiers

* Only fixed terms are currently supported, such as **24h**, **72h**, and **168h**
* `trigger_percent`
  * **Double Profit**: 10% to 100%
  * **Zero Loss**: 100%
* `payout_percent`
  * **Double Profit**: 100%
  * **Zero Loss**: 10% to 100%

***

### Supported markets

* **BTC-USD**, **ETH-USD**, and others. The UI or API response is the source of truth.

***

### Agreement

* Before buy, renew, or open-and-insure, the user must accept the required version of the [**Insurance Product Agreement**](../risk-and-policy/insurance-product-agreement/).

***

### Related pages

* [**Policy life cycle**](policy-life-cycle.md)
* [**Trigger conditions**](trigger-conditions.md)
