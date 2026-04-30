---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/feng-xian-yu-zheng-ce/bao-xian-chan-pin-xie-yi/bao-fei-tui-bao-fei-yong-yu-jie-suan-fang-shi
---

# Premium Payment, Surrender Fees, and Settlement Methods

### Premiums

* Premiums for products such as **Double Profit Insurance** can change in real time with market conditions. Always rely on the quote shown on the purchase screen before confirmation.
* Premium design can include components such as a fair premium and a risk premium. Whether each part is refundable, and how the remaining-time ratio applies, follows [Refund rules](../../insurance/refund-rules.md).

***

### Cancellation by the user

* When a user sends `cancel` for an **active** policy, the policy usually moves through **`refunding` → `cancelled`**. The system returns the refundable portion under the published rules. Very small amounts can end with no fund movement because of rounding.
* **`renew`** uses **replace** semantics. The system refunds the old policy first and then creates a new one. It does not simply extend the original expiry time.

***

### Settlement and payment

* Payouts can enter a queue. States can include pending, paid, blocked by switch, or waiting for funding. Do **not** treat the front end alone as proof that funds arrived. Use your account ledger and on-chain records.
* **Open and insure** usually uses **atomic** semantics. The position and the linked policy succeed together or fail together. See [Policy life cycle](../../insurance/policy-life-cycle.md).

***

### Related pages

* [Refund rules](../../insurance/refund-rules.md)
* [Disclaimer and Applicable Law](disclaimer-and-applicable-law.md)
