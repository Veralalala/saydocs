---
metaLinks:
  alternates:
    - https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/jiao-yi
---

# Trading

This section explains how trading works on SayFi.

Use it to understand pricing, order behavior, margin, funding, liquidation, and fees before you trade real size.

***

### What this section includes

#### [CFD overview](cfd-overview.md)

Explains the product model behind SayFi perpetuals:

#### [Pricing](pricing.md)

Explains where the mark price comes from and how the platform handles stale or invalid quotes:

#### [Order](order.md)

Explains market orders, limit orders, TP and SL behavior, and how slippage works:

#### [Position & Margin](position-and-margin.md)

Explains isolated positions, margin usage, unrealized PnL, and liquidation-price movement:

#### [Funding](funding.md)

Explains the hourly funding mechanism between longs and shorts:

#### [Liquidations](liquidations.md)

Explains when forced closure can happen and what actions reduce liquidation risk:

#### [Fees](fees.md)

Explains trading fees, slippage-related execution logic, and liquidation-penalty reservation:

***

### Recommended reading order

1. Start with [**CFD overview**](cfd-overview.md).
2. Continue with [**Pricing**](pricing.md) and [**Order**](order.md).
3. Then read [**Position & Margin**](position-and-margin.md), [**Funding**](funding.md), and [**Liquidations**](liquidations.md).
4. Finish with [**Fees**](fees.md).

***

### Core principles

* SayFi uses **USDC-settled perpetuals** with **isolated margin**.
* Mark price drives risk checks, unrealized PnL, funding, and liquidation logic.
* The assistant helps you express intent, but you still confirm sensitive trading actions.
