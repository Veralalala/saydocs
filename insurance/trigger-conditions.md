---
description: >-
  This page explains when Zero Loss and Double Profit policies become triggered,
  or instead end through cancellation and refund, based on market and position
  events.
metaLinks:
  alternates:
    - https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/bao-xian/chu-fa-tiao-jian
---

# Trigger conditions

### Trigger price

* **Zero Loss** derives `triggerPrice` on the **loss side** from inputs such as `entryPrice`, `margin`, and `trigger_percent`.
* **Double Profit** derives `triggerPrice` on the **profit side** from inputs such as `entryPrice`, `margin`, and `trigger_percent`.

If the user does not set TP or SL, the system can use **`triggerPrice`** as the effective stop or take-profit boundary.

***

### Zero Loss — when an insured event is triggered

* The position has an **active Zero Loss** policy.
* Risk control closes the **entire position** around **`triggerPrice`**.

If the same position also has Double Profit, and this close event is attributed to the **Zero Loss** path, the active **Double Profit** policy is cancelled and refunded.

If margin remains after preventive closure or hard liquidation, the product design may return part of that remaining value to the user according to `payout_percent`.

***

### Double Profit — when an insured event is triggered

* The close reason is **`INS_TAKE_PROFIT`**, which means **insurance-triggered take-profit**.
* The close is not caused by a user-defined TP firing first.
* The position has an **active Double Profit** policy.

In that case, Double Profit enters **`triggered`** and the policy benefit settlement flow starts.

If the same position also has Zero Loss, and **`DOUBLE PROFIT`** triggers first, the active **Zero Loss** policy is cancelled and refunded.

***

### Mutual exclusivity for one close event

Within one position close event, **two policy types cannot trigger at the same time**. The event is either a **Zero Loss** path on the liquidation or prevention side, or a **Double Profit** path on the insurance take-profit side.

***

### Common cases that end a policy without payout

* **Maturity without trigger** — see [**Policy life cycle**](policy-life-cycle.md)
* **User full close, non-insurance TP or SL fills first, or liquidation without a Zero Loss payout path** — see [**Refund rules**](refund-rules.md)

***

### Related pages

* [**Products**](products.md)
* [**Policy life cycle**](policy-life-cycle.md)
* [**Refund rules**](refund-rules.md)
