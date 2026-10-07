# FX (Foreign Exchange Margin Trading) Notes

🇯🇵 [日本語版](./fx.md)

Notes on FX (foreign exchange margin trading), organized from both a
mechanics and an operations perspective. Examples: USD/JPY, EUR/USD,
and other currency pairs. The first half (sections 1–6) covers how
trading works; the second half (sections 7–13) looks inside the
broker — the operational flow that supports each trade. This note
pairs with the [CFD note](./cfd.en.md) and focuses on the terms and
practices that are specific to FX.

## Contents

- [x] 0 Introduction: why FX gets its own note

### How trading works
- [ ] 1 FX market structure (the interbank market)
- [ ] 2 How to read a currency pair
- [ ] 3 Pips, trade units, and P&L calculation
- [ ] 4 Leverage and margin regulation
- [ ] 5 Swap points and rollover (how they differ from CFD rollover)
- [ ] 6 24-hour trading and liquidity risk

### Inside the broker
- [ ] 7 How are rates generated? (LP aggregation)
- [ ] 8 Cover deals and internal netting (internalization)
- [ ] 9 Post-trade processing and settlement infrastructure (matching, reconciliation, and CLS settlement)
- [ ] 10 Client asset protection and regulatory compliance (client fund segregation via trust and regulatory reporting)
- [ ] 11 Risks and operations in abnormal conditions
- [ ] 12 A-book/B-book and how brokers make money
- [ ] 13 Working with the PB (prime broker)

---

## 0 Introduction: why FX gets its own note

FX is a CFD on currencies (currency pairs). Within the broad CFD
category, FX sits alongside equity indices and commodities.

Even so, in practice FX is usually handled as a separate product from
other CFDs. The main reasons are:

| Aspect | What's specific to FX | See |
|---|---|---|
| Market size | Japan is one of the world's largest markets for retail FX by trading volume, and it is correspondingly subject to many regulations | 4, 10 |
| Pricing | The reference price isn't an exchange-traded future but the spot price set through bilateral trading between financial institutions. With no contract months, there's no contract-month rollover as with CFDs. Instead, FX brokers roll the settlement date forward every day (a rollover), which gives rise to swap points | 1, 5 |
| Trading hours | Trading runs almost 24 hours on weekdays, so brokers need to be ready for price gaps over the weekend and for liquidity that changes by time of day | 6 |
| Counterparties | Multiple LPs (liquidity providers: financial institutions that quote tradable prices) act as price sources, and separately there's a PB (prime broker) where positions are held. With this many counterparties (CPs) involved, the setup is complex | 7, 8, 13 |
| Settlement | Cover trades involve actual delivery of currencies, so post-trade work such as matching, reconciliation, and CLS settlement carries a lot of weight | 9 |
| Regulation | Leverage caps, trust-based protection of client funds, regulatory reporting, and more are set out in particular detail for FX | 4, 10 |
| Brokers and trading style | Many brokers specialize in FX and compete hard on tight spreads (the gap between the bid and ask prices). Short-term and automated trading are common, so fast rate distribution and execution matter | 7 |
| Relationship to CFDs | The yen-conversion rate used when trading overseas CFD products in yen is itself an exchange rate. FX is also the foundation that supports CFD operations | [CFD Notes: Basics](./cfd-basics.en.md) |

Many of the basic ideas in FX are shared with CFDs. The following
topics are explained in the [CFD notes](./cfd.en.md), so this note
doesn't repeat them in detail. Read them first as needed.

| CFD notes topic | Related FX section |
|---|---|
| ["What is cash settlement?"](./cfd-basics.en.md) | The whole note |
| ["Long and short"](./cfd-basics.en.md) | 2, 3 |
| ["Leverage and margin"](./cfd-basics.en.md) | 4 |
| ["How are rates generated?"](./cfd-pricing-and-cover.en.md) | 7 |
| ["The idea behind cover deals"](./cfd-pricing-and-cover.en.md) | 8 |
| ["Position limits and cover strategy"](./cfd-pricing-and-cover.en.md) | 8 |
| ["What is a rollover?"](./cfd-rollover-and-adjustments.en.md) | 5 (to compare with CFDs) |

The first draft of this note is kept for reference in
[fx-v1.en.md](./fx-v1.en.md). It will be deleted once this note is
complete.
