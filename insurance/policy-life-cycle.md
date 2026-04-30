---
description: >-
  This page explains how a policy moves from creation to completion through
  states and user actions.
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/bao-xian/bao-dan-sheng-ming-zhou-qi
---

# Policy life cycle

| State       | Meaning                                                                                                                                                     |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `active`    | Coverage is in progress                                                                                                                                     |
| `refunding` | The refund flow has started and is waiting for settlement                                                                                                   |
| `expired`   | The policy reaches maturity **without a trigger** and ends naturally                                                                                        |
| `triggered` | An **insured event is confirmed** and the policy enters payout processing                                                                                   |
| `cancelled` | The policy ends for a non-payout reason, such as user cancel, replacement, position closure, or system cancel. It usually passes through `refunding` first. |

***

### User actions and semantics

* **`buy`**: Create a **new policy** when the position does **not** already have an active policy of that type.
* **`renew`**: If an active policy already exists, the system follows **cancel old, then create new**. Coverage starts from the **new policy**. It does not extend the old policy in place.
* **`cancel`**: Actively cancel an active policy. The usual path is `active` → `refunding` → `cancelled`.

***

### Typical paths

* **Normal holding**\
  `active` → matures without trigger → `expired`\
  This is a `NO_TRIGGER` outcome. On expiry, the premium is usually **not refunded**. See [**Refund rules**](refund-rules.md).
* **Payout trigger**\
  `active` → trigger conditions are met → `triggered`
* **Cancel, replace, or close-driven cancellation**\
  `active` → `refunding` → `cancelled`

***

### Relation to the position life cycle

* A full close, user TP or SL, or liquidation without an insurance-triggered payout can **passively cancel** the active policy and start a refund flow.
* When one policy is triggered through Zero Loss or Double Profit, the active policy of the other type on the same position enters the paired cancel-and-refund path.

***

### Related pages

* [**Product**](product.md)
* [**Trigger conditions**](trigger-conditions.md)
* [**Refund rules**](refund-rules.md)
