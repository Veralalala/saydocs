---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/feng-xian-yu-zheng-ce/bao-xian-chan-pin-xie-yi/xie-yi-xiu-ding-yu-sheng-xiao-gui-ze
---

# Agreement Amendments and Effective Rules

### Amendments

The platform can update insurance terms, pricing parameters, or technical rules for reasons such as regulation, risk control, actuarial changes, or product iteration. Changes are usually published through:

* **In-app notices**, with the version number, effective time, summary, or full text.
* **The documentation site**.

***

### Effective rules and active policies

| Scenario                                      | General rule                                                                                                                                                                                                                                                                                                |
| --------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **An active policy that is already in force** | The system usually follows the agreement version and parameter snapshot stored at underwriting time, such as `payout_amount`, expiry time, and trigger thresholds. Later wording or parameter updates do not unilaterally change already locked economic terms unless the formal legal text says otherwise. |
| **New purchase or renewal**                   | A renewal usually uses **replace** semantics. The old policy ends first, including refund handling, and the new policy takes effect under new pricing and terms. See [Policy life cycle](../../insurance/policy-life-cycle.md).                                                                             |
| **Forced delisting or circuit breaker**       | Operations can restrict **new underwriting**, such as `insurance_enabled` switches or market-level breakers. That does **not automatically remove** obligations that already exist, but execution can still depend on payout switches, available funds, and other formal rules.                             |

***

### Related pages

* [Scope of Application and Definition of Parties](scope-of-application-and-definition-of-parties.md)
