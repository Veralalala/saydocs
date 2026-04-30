---
icon: circle-baht
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/ai-jiao-yi-yuan/zi-zhang-hu-yu-qian-bao
---

# Sub-account wallets

SayFi uses a **multi-AI-Trader** structure. Each Trader maps to **one independent sub-account**. The multi-wallet or multi-account experience in the sidebar is really a set of isolated margin pools and positions. This works well for strategy separation and different risk preferences, while funds remain **self-custodied on-chain**.

***

### What a sub-account is

* **One Trader = one sub-account**\
  Each sub-account has its own margin pool and **isolated** positions. Losses or liquidation in one sub-account do **not** automatically affect others.
* **Fund isolation**\
  USDC and positions in sub-account A are separate from sub-account B. You can treat each Trader as a separate capital bucket.
* **Conversation isolation**\
  Each Trader keeps its own chat history and assistant context. Multi-strategy discussions stay cleaner.

Current product limits:

* Each user can create up to **10** sub-accounts.
* Contracts are **USDC-settled perpetuals**.

***

### Relationship to your wallet

* **You still control the funds**
* **Login and signing**\
  Whether you use **MetaMask**, **WalletConnect**, **Rabby**, or a social-login flow supported by the product, real trades and fund actions still rely on on-chain authorization and signatures. Natural language is the interface layer. It does not bypass your signing authority.
* **Convenience and delegated signing scenarios**\
  For smoother interaction, the product can apply practices such as encrypted key storage, permission isolation, and minimal exposure. Final implementation details follow official security disclosures and the live interface.

Before large actions, verify the approval scope and contract address in both the wallet and the trading interface.

***

### Common use cases

| Scenario                                         | Suggested setup                                                                                    |
| ------------------------------------------------ | -------------------------------------------------------------------------------------------------- |
| Testing a new strategy                           | Create a new Trader and start with small size in a separate sub-account.                           |
| Separating long-term and short-term trading      | Use two Traders with separate funds and separate chat context.                                     |
| Avoiding confusion about which account is active | Confirm orders inside the same Trader chat. Check the current Trader and balance before switching. |

***

### Security reminders

* SayFi does **not** use a traditional private customer-service flow that asks for your private key, mnemonic, transfers, or paid account recovery.
* If you have questions about positions or funds, verify them through the app and on-chain records.
