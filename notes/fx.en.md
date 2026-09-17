# FX (Foreign Exchange Margin Trading) Notes

🇯🇵 [日本語版](./fx.md)

Notes on FX (Foreign Exchange margin trading), organized from both a
mechanics and an operations perspective. This note pairs with the
[CFD note](./cfd.en.md) and focuses on the terms and practices that are
specific to FX.

---

## What FX Is

FX stands for "Foreign Exchange" — margin trading on currency pairs
such as USD/JPY or EUR/JPY, where you aim to profit from changes in
the exchange rate between the two currencies.

FX is actually a type of the "CFD (Contract for Difference)" described
in the [CFD note](./cfd.en.md). If a CFD in general is "a trade that
settles only the price difference, with no delivery of the underlying
asset," then FX is the CFD version of that idea applied to currency
pairs. CFD is the umbrella term, and stock indices, commodities, and
FX all sit under it.

The main way FX differs from other CFD products (such as CFDs based on
stock-index or commodity futures) is the price it references. Instead
of an exchange-traded futures price, FX references the spot price
formed through over-the-counter (OTC) dealing directly between
financial institutions. Because there is no exchange involved, FX has
no concept of a futures expiry ("limit month") or rollover, and it
trades almost 24 hours a day on weekdays.

## How Price and P&L Work

To understand P&L in FX, it helps to know at least these four terms.

### Pips

A pip is the common unit used to express price movement in a currency
pair. For most pairs — such as USD/JPY — 1 pip equals 0.01 yen (there
are exceptions where the unit is defined differently, such as some
pairs quoted against the euro or pound). Rather than talking about
price moves in raw yen or dollar amounts, which would differ pair by
pair, pips give traders a common ruler to compare price movement
across currency pairs.

### Leverage

Leverage lets you trade a position many times larger than the funds
(margin) you actually put down. This is the FX-specific term for the
same idea the CFD note describes as "settling only the price
difference lets you trade with less capital." For example, with 25x
leverage, 100,000 yen of margin lets you control a position worth
2.5 million yen. Trading a larger position with less capital also
means both gains and losses are magnified by the same multiple — see
"Common Pitfalls" below.

### Margin

Margin is the collateral you deposit into your trading account in
advance in order to trade with leverage. The margin itself is not the
capital used to make the trade; it exists as collateral in case a
large loss occurs. As the unrealized P&L on your open positions moves,
your margin level (the ratio of equity to required margin) moves with
it, and if that level falls below a certain threshold, a forced
liquidation ("margin call" / stop-out) is triggered.

### Swap Points

Swap points are the gain or loss that arises from the interest-rate
differential between the two currencies in a pair. Because an FX trade
is effectively "buying one currency while selling the other," a
position that sells the lower-interest-rate currency and buys the
higher-interest-rate one earns that interest differential each day it
is held (the opposite combination results in a daily payment instead).
Swap points accrue each time a position is carried over to the next
day, and — as covered under "Common Pitfalls" below — they can be
either a receipt or a payment.

## How It's Handled in Practice

When a broker quotes FX rates to clients, two practices are typically
involved: how the rate itself is generated, and how the broker manages
its own resulting risk.

### How rates are generated

Since FX has no exchange-traded futures price like the one described
in the CFD note, brokers instead generate their own internal rates
based on the interbank rate — the rate formed in the interbank market,
where banks trade currencies with one another. The general flow is:
start from the interbank rate, then add a spread (the difference
between the bid and ask price) and adjustments reflecting the broker's
own risk position to arrive at the rate quoted to clients. The reason
the same currency pair can show slightly different rates at different
brokers comes down to differences in how each one sets its spread and
builds its rate feed.

### The idea behind cover deals

When a client buys (or sells) a currency pair, the broker ends up
holding the opposite position. Left unmanaged, this would leave the
broker itself exposed to currency risk. To offset this, the broker
executes an opposite trade in the interbank market (or similar venues)
to cancel out its own inventory risk — this is called a cover deal.
The purpose of a cover deal is not for the broker to profit from
currency movements itself, but purely to manage the inventory risk
created by the position it took on from the client.

## Common Pitfalls

Here are some points that are easy to misunderstand when first
learning about FX.

- **Swap points can be a payment, not just a receipt.** A position
  that buys the higher-interest-rate currency and sells the
  lower-interest-rate one earns swap, but the opposite combination
  (buying the lower-interest-rate currency and selling the
  higher-interest-rate one) means you pay swap instead. Assuming
  "swap always means income" can hide an unexpected ongoing cost.
- **Leverage is capped by domestic regulation.** For individuals
  trading through a Japan-based FX broker, leverage is capped by the
  Financial Services Agency (at the time of writing, a maximum of 25x
  for retail clients). This cap is a general figure that can change
  with future regulatory revisions, so treat it as a general
  reference point rather than a fixed constant.
- **A "gap" can occur at the start of the week.** The FX market runs
  almost 24 hours a day on weekdays, but it is closed over the
  weekend. If major news breaks while the market is closed, the rate
  on Monday morning can open at a level sharply discontinuous from
  Friday's close — a "gap." Anyone carrying a position over the
  weekend should keep this gap risk in mind.
- **Falling margin levels trigger a forced liquidation.** If
  unrealized losses grow and your margin level drops below a certain
  threshold, your position is closed automatically, regardless of
  your own intent. The higher the leverage used, the less price
  movement it takes to reach that threshold.

---

This note is a personal study record intended to explain general
financial concepts. It is not investment advice.
