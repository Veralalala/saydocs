---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/feng-xian-yu-zheng-ce/feng-xian-pi-lu/bao-xian-bu-cheng-bao-qing-xing-yi-lan
---

# List of scenarios not covered by insurance

## List of scenarios not covered by insurance

This page summarizes situations where **Zero Loss Insurance** or **Double-Profit Insurance** typically does **not** pay out, or where the policy ends through **cancellation or refund instead of payout**. These cases should stay consistent with [Trigger conditions](../../insurance/trigger-conditions.md) and [Refund rules](../../insurance/refund-rules.md). The formal insurance terms always control.

***

### Common non-payout scenarios

| Scenario                                                                   | Explanation                                                                                                                                                                                 |
| -------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **The policy expires before the agreed condition is reached**              | The policy moves to `expired`. Premiums are usually **not refunded** at expiry.                                                                                                             |
| **The user fully closes the position**                                     | The policy ends with the position and usually refunds under reasons such as `CLOSE`. This is **not** an insurance payout event.                                                             |
| **A regular TP or SL triggers before the insurance price**                 | The close reason does not follow the insurance-led path. The policy usually cancels and refunds under the matching reason.                                                                  |
| **Liquidation happens but not through the Zero Loss payout path**          | If Zero Loss trigger semantics are not met, the position can be handled as a regular liquidation. Zero Loss Insurance does **not** pay under the full-margin restoration path in that case. |
| **Double-Profit Insurance does not trigger through the insurance TP path** | If profit-side attribution does not follow the agreed path such as `INS_TAKE_PROFIT`, the policy does not enter the `triggered` payout flow.                                                |
| **Another policy on the same position already became the primary trigger** | One close event can have only one primary trigger. The other active policy usually cancels and refunds. It does not create a double payout.                                                 |

***

### System and operational limits

* **New-underwriting circuit breakers** usually restrict **new policies**. Whether they affect historical obligations still follows the formal terms.
* **Unsupported markets** cannot be insured.

***

### Related pages

* [Identifying Insured Events and Exclusion Clauses](../insurance-product-agreement/identifying-insured-events-and-exclusion-clauses.md)
* [Instructions for handling insufficient funds in extreme market conditions](instructions-for-handling-insufficient-funds-in-extreme-market-conditions.md)
