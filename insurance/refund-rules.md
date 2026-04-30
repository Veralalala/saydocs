---
description: >-
  This page explains refund scenarios, calculation principles, and refund reason
  values for insurance policies.
metaLinks:
  alternates:
    - https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/bao-xian/tui-fei-gui-ze
---

# Refund rules

### When refunds happen

* **User-initiated cancel** (`USER_CANCEL`)
* **Renewal or parameter replacement** (`POLICY_REPLACE`) — refund the old policy first, then create the new one. In practice, `renew` uses replace semantics.
* **System-forced cancel** (`SYSTEM_CANCEL`)
* **Position changes that make the policy no longer applicable** — for example, user full close, non-insurance TP or SL triggers first, or liquidation without the Zero Loss payout path

> If a policy reaches **`expired`** without a trigger, the premium is **not refunded**.

***

### State path

* The default refund path is `active` → **`refunding`** → **`cancelled`**
* If the policy has already expired, or if **remaining fair premium + refundable risk-return portion ≤ 0**, no refund event is generated

***

### Calculation principles

* **Remaining fair premium**: Calculated from remaining time together with market data and option-style pricing inputs
* **Risk-return portion**: The refundable part of the premium's risk-return component is returned according to **remaining time**
* **Non-refundable portion**: One-time or execution-related costs such as `fundingFee`, `liqFee`, and `closeFee` are not refunded

> This page does not include audit-level formula details, line-item definitions, or implementation edge cases.

***

### Refund `reason` values

Each `refund event` should distinguish:

* `USER_CANCEL` — user-initiated cancel
* `POLICY_REPLACE` — renewal or tier replacement
* `SYSTEM_CANCEL` — system, risk-control, or agreement-driven forced cancel
* `CLOSE` — user close or a **normal** TP or SL causes linked cancellation
* `LIQUIDATION` — liquidation-linked cancellation, or cancellation of **Double Profit** when **Zero Loss** pays out
* `TAKE_PROFIT` — cancellation of **Zero Loss** when **Double Profit** pays out

***

### Renewal and tier change

* Renewal or tier change means **refund the old policy first, then create a new one**. The old policy ends. The new policy is priced again from scratch.

***

### Related pages

* [**Policy life cycle**](policy-life-cycle.md)
* [**Trigger conditions**](trigger-conditions.md)
* [**Pricing model**](pricing-model.md)
