# CFD Notes: Basics

🇯🇵 [日本語版](./cfd-basics.md)

[← Back to the CFD notes index](./cfd.en.md)

This file covers the basic mechanics of CFDs: what a CFD is, why it
exists as a product, leverage and margin, cash settlement, and long
and short positions.

---

### What is a CFD?

A CFD is one type of financial derivative. A derivative is a contract
whose value is derived from (depends on) the price of an underlying
asset. The three basic types — often called the "big three"
derivatives — are:

- Futures: a contract to buy or sell a specific asset at a price
  agreed today, for delivery/settlement on a set future date (e.g.,
  Nikkei 225 futures)
- Options: the right (not the obligation) to buy or sell a specific
  asset at a price agreed today, exercisable on a set future date
- Swaps: an agreement between two parties to exchange different cash
  flows (e.g., interest rates, currencies) over a period

A CFD (Contract for Difference) is a separate type of derivative from
these three. Its defining feature is that there's no physical
delivery: only the difference between the entry and exit prices is
settled. That said, settling only the difference isn't unique to
CFDs. Nikkei 225 futures, for example, are ultimately settled not by
delivering the underlying but by paying the difference in cash
(cash settlement against the Special Quotation (SQ), the final
settlement price).

"CFD" stands for "Contract for Difference." In Japanese it's called
差金決済取引 (sakin-kessai torihiki) — literally "trading settled by
the difference."

"Cash settlement" here means no physical delivery of the underlying
(a stock, oil, a stock index, etc.) ever happens — only the price
difference from entry to exit changes hands. For example, if you buy
at 100 and sell at 120, you never actually receive 100 worth of the
underlying or hand over 120 worth of it; only the 20 difference is
settled.

FX (foreign exchange trading), which you've probably heard of, is
actually a type of CFD too — you can think of FX as "a CFD on a
currency pair." CFD is the umbrella category, and equity indices,
commodities, and FX all sit inside it.

A CFD is an over-the-counter (OTC) product: the broker (dealer) and
the client enter into a one-to-one contract without going through an
exchange. In Japanese this is also called 相対取引 (aitai torihiki),
i.e., bilateral trading.

Note that exchange-traded CFDs also exist (for example, "Click Kabu
365" on the Tokyo Financial Exchange). These notes assume OTC CFDs,
where the broker and the client contract with each other directly.

In exchange trading (say, exchange-traded equities), many buyers' and
sellers' orders sit together in an "order book," and price is set by
that supply and demand. A CFD doesn't use an order book at all — the
client trades against a price (rate) that the broker itself quotes.
This difference gives rise to a few characteristics:

- Because there's no rigid exchange-style specification (lot sizes,
  expiry dates, and so on), the broker has room to set terms
  flexibly. This flexibility is also why "rollover" exists as a
  concept for CFDs — the broker can roll a position forward on its
  own even though the underlying futures contract it references has
  a fixed contract month (see ["Rollover"](./cfd-rollover-and-adjustments.en.md)).
- The broker quotes a bid (the price at which the client can sell)
  and an ask (the price at which the client can buy), and the
  difference between them — the spread — is effectively the cost of
  the trade.
- Because there's no exchange or clearing house guaranteeing
  settlement, there's a risk that the counterparty (the broker)
  could fail to honor the contract, e.g., through insolvency
  (counterparty risk).

How the spread gets decided, and how the broker deals with the risk
it picks up from trading with clients, are covered later under ["How
are rates generated?"](./cfd-pricing-and-cover.en.md) and ["The idea behind cover deals."](./cfd-pricing-and-cover.en.md)

#### Why can you trade without holding the underlying?

A CFD is built by referencing the price of an underlying asset (a
stock or commodity itself, or its futures), but it doesn't require
the full amount of capital that buying the physical asset outright
would. Since a CFD only settles the price difference, it lets you
trade with less capital (this connects to the idea of leverage,
covered in its own section).

Trading the physical asset or its futures also comes with the
hassle of delivery. For example, if you trade WTI crude oil futures
and keep holding the position past its contract month (the month in
which the contract expires), delivery of the physical asset (crude
oil itself) would normally be triggered. To avoid that, you'd have to
roll over to the next contract month yourself before expiry. With a
CFD, the broker handles all of that delivery and rollover work on the
client's behalf, so the client can focus purely on the cash-settled
trade without ever having to think about the physical asset.

On top of that, trading on an exchange is only possible while that
exchange is open. CFD trading hours are set by the broker and often
follow the reference market's hours. Depending on the broker and the
product, you may also be able to trade while domestic exchanges are
closed.

#### A concrete example: what is a CFD actually referencing?

What a CFD's price actually tracks depends on the product type.

- Japan 225: tracks the price of Nikkei 225 futures as traded on an
  exchange. Which exchange is used as the reference varies by
  broker, but Osaka Exchange, SGX (Singapore Exchange), and CME
  (Chicago Mercantile Exchange) are common examples.
  The reason a CFD on the Nikkei Stock Average goes by a name like
  "Japan 225" is generally explained as follows: "Nikkei Stock
  Average" and "Nikkei 225" are trademarks of Nikkei Inc., and using
  those names in a product name requires Nikkei's permission (a
  license). As a result, the name varies by broker — "Japan 225,"
  "Japan N225," "JP225," and so on.
- WTI Crude Oil: similarly, tracks the price of WTI crude oil futures
  traded on an exchange.
- ETF-type CFDs, such as a US semiconductor ETF CFD: tracks the
  price of the ETF itself. A CFD on a US semiconductor ETF, for
  example, tracks the actual price movement of a real ETF like the
  iShares Semiconductor ETF. Note that buying the ETF itself and
  trading a CFD that references it are two different things (see
  Note ① below).
- Products with no exchange involved, like FX or spot gold: tracks
  the spot price, which is set through direct bilateral trading
  between financial institutions rather than on an exchange (see
  Note ② below). Note that some precious-metal CFDs reference
  futures instead (see ["Examples by Product Type"](./cfd-product-types.en.md)).

So depending on the product, a CFD is built on top of one of three
types of reference price: futures, an ETF, or a spot rate. The cash
settlement mechanism described above is common to all of them, but
what sits behind that mechanism is not uniform — that's the key
point.

---
Note ①: What is an ETF?

An ETF (Exchange Traded Fund) is a financial product designed to
track a stock index or commodity. The fund manager pools investor
capital to buy the underlying constituent stocks, so buying the ETF
gives you the same effect as being diversified across those
constituents (and you can receive distributions in place of
dividends). Buying the ETF itself requires the full purchase amount
and means you actually own (a share of) the underlying asset. A CFD,
by contrast, never involves owning the physical asset, so no
shareholder rights arise — it's purely a trade that settles the
difference between your entry price and your exit price.

Note ②: What is spot trading?

Spot trading is a trade where physical delivery is completed within
a short period after the trade is agreed (normally within two
business days). It doesn't go through an exchange — the price is
based on rates exchanged directly between financial institutions.

#### Where do I (in operations) fit into a CFD?

Keeping a CFD product running touches many different areas of
operations work. Here's the overall picture; the details of each
area are covered in their own sections (rollover, leverage and
margin, etc.).

- Market and risk management: monitoring market conditions (circuit
  breakers, stock-borrowing restrictions, etc.), assessing and
  adjusting client position risk, monitoring risk exposure, watching
  for stop-outs (forced liquidation), and checking quoted rates for
  anomalies
- Product operations: handling corporate actions (new listings,
  spin-offs, stock splits, mergers, etc.), tracking exchange
  schedules, determining and applying price adjustment amounts,
  rolling contract months over, and hedging
- Administration and compliance: reconciliation (matching the books
  against actual balances), verifying segregation of client assets,
  preparing reports for regulators and industry bodies (the Financial
  Services Agency (FSA), the Financial Futures Association of Japan
  (FFAJ), etc.), and handling
  KYC (know your customer) / AML (anti-money laundering)
- System operations: incident response, maintaining fallback
  procedures under the business continuity plan (BCP), and
  pre-release testing (UAT) for new products

In short, keeping a single CFD product running requires several
roles working together: getting the price right, managing risk,
staying compliant, and keeping systems running reliably.

#### Where I would have stumbled three years ago

By this point, a lot of terms — CFD, FX, ETF, futures, spot trading
— have come up all at once. Rather than trying to understand
everything together, it helps to pick one product and go deep on
that first.

With WTI crude oil, for example, you can follow one thread: "the
rate is built from a futures price that has a contract month" →
"when the settlement date arrives, a rollover is normally required"
→ "operations handles that hassle on the client's behalf, so the
client can keep trading without doing anything." Once you understand
that chain for one product, it carries over to the others. The thing
underneath it all is that a CFD is always a trade based on a price
difference, with no physical delivery.

A few other misconceptions beginners often run into:

- Assuming "trading with less capital" means "borrowing money": a
  CFD isn't a loan — it lets you trade with less capital precisely
  because it only settles the price difference.
- Assuming a CFD's price exactly matches the futures or ETF price it
  references: a CFD's price includes things like the spread (the gap
  between the bid and ask), so it can differ slightly from the
  reference price (see Note ③ below).
- Assuming that trading a stock or ETF via CFD means you "bought the
  stock": since a CFD never involves owning the physical asset, none
  of the rights that come with being a shareholder (voting rights,
  shareholder perks, etc.) apply.

Note ③: What is the spread (offer / bid)?

A CFD's price is always quoted as two values side by side. With a
CFD, the party quoting both prices is the broker.

- Ask (offer): the price at which the other side is willing to sell.
  If you're buying, this is the price you buy at.
- Bid: the price at which the other side is willing to buy. If you're
  selling, this is the price you sell at.

The ask (the seller's asking price) is normally higher than the bid
(the price the buyer is willing to pay). The gap between the two is
the "spread," and it's the CFD's real trading cost.

### Why does a CFD exist as a product? (How it differs from the physical asset)

Trading the physical asset means owning the asset itself — stocks,
bonds, currencies, interest-rate instruments, gold, oil, and so on —
and buying or selling it involves actual delivery of that asset.

A CFD treats that same underlying asset as its "reference" and only
settles the price difference. With a CFD, there's no delivery of the
underlying, and none of the rights that come with it (like
shareholder rights) ever arise.

#### Why trade a CFD instead of buying the physical asset?

Compared with trading the physical asset, a CFD offers several
advantages:

- No trading commission: CFDs are usually commission-free (the
  spread is the real cost instead).
- No physical delivery: since only the price difference changes
  hands, there's no storage, transport, or delivery hassle at all.
- Leverage: a small amount of margin gives you the same effect as
  trading a much larger position.
- Easier to short: you can't sell the physical asset without holding
  it first, but a CFD can be opened with a new short position, so you
  can aim to profit even when prices are falling.
- One account across products and markets: products that would
  normally require separate accounts — Japanese stocks, US stocks,
  oil, FX — can all be traded from a single account.
- No need to open an overseas brokerage account: you can trade CFDs
  on US stocks or overseas commodities from Japan, for example,
  without the hassle of opening an account with a local broker.
- Smaller trade sizes: physical stocks often have to be bought in
  round lots (e.g., 100-share units), whereas CFDs can often be
  traded in smaller units.
- Dividend-equivalent adjustments (for single-stock and ETF CFDs):
  you're not a shareholder, but you still receive an adjustment
  amount equivalent to the dividend when one is paid (and pay the
  equivalent if you're short). For equity index CFDs that reference
  futures, the dividend is already priced into the futures and is
  settled through the price adjustment at rollover instead (see
  ["Examples by Product Type"](./cfd-product-types.en.md)).
- Longer trading hours: depending on the broker and the product, you
  aren't tied to domestic exchange hours and can trade overnight,
  including on overseas markets.

#### A concrete example: how do physical WTI crude oil, WTI futures, and a WTI CFD differ?

To see the difference concretely, compare three things: physical WTI
crude oil, WTI crude oil futures, and a WTI crude oil CFD. Futures are
included because what a WTI crude oil CFD references is the futures
price, not the physical price — and contract months and rollover are
properties of futures in the first place.

| Item | Physical WTI crude oil | WTI crude oil futures | WTI crude oil CFD |
|---|---|---|---|
| What's traded | The crude oil itself (actually owned) | A promise to deliver crude oil on a future date (a contract per contract month) | A contract that references the futures price and settles only the price difference |
| Delivery / rollover | You receive the crude oil when you buy it; there's no concept of a contract month | Holding to expiry triggers delivery of crude oil; avoiding it requires rolling over to the next contract month yourself | No delivery ever happens; the broker handles the rollover on your behalf |
| Capital required | The full trade amount | Margin only (leverage applies) | Margin only (leverage applies) |
| Short selling | You can't sell crude oil you don't hold | Can be opened directly as a new short position | Can be opened directly as a new short position |
| Trade size | Mostly large-lot trading; buying and selling small amounts isn't realistic for individuals | Large size per contract | Often tradable in smaller units than futures |
| Trading hours | No fixed exchange hours (mostly traded bilaterally) | Limited to the futures exchange's hours | Hours set by the broker (often following the referenced futures' hours) |
| Storage / incidental costs | Storage and transport costs apply | No storage costs, but trading fees and the cost of trading at rollover apply | No concept of storage; costs are folded into things like the spread and price adjustments at rollover |

So even though the underlying price movement is the same, the
differences arise in two steps. Going from physical to futures adds
flexibility — "no need for the full amount of capital," "you can
start with a sell" — but because futures have contract months, you
now have to manage delivery and rollover yourself. A CFD references
the futures price while having the broker take on that delivery and
rollover work, so the client doesn't have to think about either
"whether to hold the physical asset" or "how to manage contract
months."

#### Where do I (in operations) notice the difference between physical and CFD trading?

Because a CFD never holds the physical asset, it creates operations
work that has no counterpart in physical trading. In practice, this
difference shows up especially in:

- Rollover (rolling the contract month): in futures trading the
  investor rolls over themselves; with a CFD, the broker does it on
  the client's behalf, so the rollover itself becomes operations work
- Managing the adjustment amount: calculating and applying the
  adjustment that offsets the price discontinuity caused by rollover
  (for single stocks and spot products, this also includes
  registering and applying rights adjustments (adjustments for
  dividends and other shareholder rights) and interest adjustments)
- Risk management: because leverage is in play, position risk can
  grow larger than in physical trading, so it needs to be monitored
  and adjusted
- Managing the reference exchange's trading hours: the broker sets a
  CFD's trading hours, but the futures or physical exchange it
  references has its own trading hours and holidays, so those hours
  and schedules need to be tracked
- Generating rates from the reference contract month's price: a
  CFD's price isn't set independently — it's generated from the
  price of the contract month it references, so that link has to be
  maintained
- Managing trade units: CFDs are sometimes traded in different units
  from the physical asset, which needs its own setup and management
- Setting and maintaining margin rates / leverage ratios: offering
  leverage means monitoring margin levels and handling cases where
  margin falls short
- Setting and monitoring stop-out levels: managing the forced-
  liquidation mechanism itself, which has no equivalent in physical
  trading
- Setting spreads: unlike physical trading, which charges a
  commission, managing the CFD-specific cost structure (the gap
  between bid and ask)
- Maintaining the contract-month master data: managing the master
  data for which contract month is referenced until when (the
  foundation that rollover depends on)
- Managing the yen-conversion rate: setting the FX conversion rate
  used when offering an overseas product priced in yen

In short, the defining feature of a CFD — not holding the physical
asset — is exactly what adds these extra management items (price,
risk, timing, units) to the operations side.

#### Where I would have stumbled three years ago

"The price moves exactly like the physical asset, so why does a
separate product called a CFD even exist?" — that might be your
first reaction. "Why not just trade the physical asset directly?"

But for a commodity like crude oil, trading the physical asset
directly requires the full amount of capital and the trouble of
storage, which isn't realistic for individuals. Trading futures
directly instead means you'd have to roll over the position yourself
every time the contract month arrives — which is a hassle, and if you
forgot, delivery of the physical asset (the crude oil itself) could
actually be triggered. A CFD exists precisely because the broker
takes on that hassle and delivery risk on your behalf.

That said, this doesn't mean "a CFD is simply the better deal." A
CFD carries its own cost — the spread (the gap between bid and ask)
— and because leverage is in play, unrealized losses can grow faster
than they would with the physical asset. "No delivery, so it's
convenient" and "lower risk" are two different things, and using a
CFD means understanding its specific costs and risks too.

### Leverage and margin

#### What is leverage, in a nutshell?

Leverage is a mechanism that lets you trade an amount many times
larger than the margin (the money you deposit as collateral) you put
up. For retail CFDs in Japan, the maximum leverage is set by
regulation for each product type: as of writing, 10x for equity
indices, 20x for commodities (oil, gold, etc.), and 5x for single
stocks and ETFs (FX is capped at 25x). These caps can change if the
rules change. The caps for CFDs on equity indices, single stocks, and
the like are set at a margin level roughly meant to cover one day's
price movement; single stocks can move sharply on one company's
earnings or news, so their cap is kept low. Commodity CFDs such as
oil and gold, on the other hand, are regulated under a different law
from equity index CFDs (the Commodity Derivatives Act), and their cap
is set separately. So you can't simply conclude that "commodities
get 20x, so they must move less than equity indices."

For example, if you deposit ¥100,000 as margin on an equity index
CFD, 10x leverage lets you trade a position worth ¥1,000,000. In
other words, even though the capital you actually put up is
¥100,000, you receive the full price movement on ¥1,000,000 as your
P&L.

#### What is margin, and how does it relate to leverage?

Margin is the money you deposit with the broker as collateral in
order to trade.

Leverage is the mechanism of trading many times the amount of that
margin, so margin and leverage are two sides of the same coin. The
ratio of the margin you actually deposit to the position size
(notional value) is called the "margin rate," and leverage is the
inverse of the margin rate (e.g., a 10% margin rate = 10x leverage).

Margin isn't just the "initial margin" needed to open a position —
it also acts as a cushion that absorbs any unrealized loss. The
ratio of your account's remaining equity (effective margin) to the
required margin is called the "margin level" (or maintenance
margin ratio). When this level falls below a certain threshold, the
broker may ask for additional margin (a margin call) or forcibly
close the position (a stop-out).

#### A concrete example: with X margin and Y leverage, how large a trade can you make?

Take a Japan 225 CFD as an example. You deposit ¥100,000 as margin
and trade at 10x leverage, the cap for equity index CFDs.

- Maximum position size: ¥100,000 × 10 = ¥1,000,000
- Margin rate: 1 ÷ 10 = 10%
- Required margin (the margin needed to trade ¥1,000,000 worth): ¥1,000,000 × 10% = ¥100,000

So "position size × margin rate" gives you the required margin, and
"margin × leverage" (or "margin ÷ margin rate") gives you the
maximum position size.

#### Where do I (in operations) step in when margin runs short (a margin call)?

The margin level is calculated as "account equity (effective margin)
÷ required margin × 100%." What happens next depends on how far the
level has dropped — but the exact thresholds and grace periods vary
by broker. The following is just one illustrative example.

- If the margin level is below 100% and carries over into the next
  business day: there's a grace period. If the client tops up margin
  (a margin call payment) or closes part of the position to bring
  the level back up before a set deadline (e.g., by the end of the
  next business day), forced liquidation of the entire position can
  be avoided. If the deadline passes without resolution, the broker
  closes the entire position.
- If the margin level falls below a certain threshold (e.g., 50%):
  there's no grace period at all. The instant it crosses that line,
  the entire position is forcibly closed (a stop-out). This also
  serves as a safeguard to keep the client's losses from growing any
  further. Note, though, that a stop-out is a mechanism that
  "triggers closing once that level is reached"; it doesn't guarantee
  the position is closed at that level's price. When the market moves
  sharply or gaps (opens far away from the previous close), the
  position can be closed at a price much worse than the stop-out
  level, creating a loss larger than the margin deposited (a
  negative balance, or deficit). In that case, the client has to
  deposit funds to cover the negative balance.

Operations continuously monitors margin levels account by account,
sends margin-call notices to accounts that cross the threshold with
a grace period, and confirms that the stop-out process has run
correctly for accounts that cross the no-grace-period threshold. For
accounts left with a negative balance after a stop-out, operations also
notifies the client and confirms the deposit.

#### Where I would have stumbled three years ago

- Assuming leverage means "trading with borrowed money": leverage
  isn't a loan — it's a mechanism for trading a multiple of your
  margin, which serves as collateral. That said, "not a loan" doesn't
  mean "you can't lose more than your margin." When the margin level
  falls below a certain threshold, the position is forcibly closed by
  a stop-out — but if the market moves sharply, the close can't keep
  up, and a loss larger than the margin (a negative balance) can
  arise, which you're obliged to pay.
- Assuming you should always use the maximum leverage available:
  being able to trade up to the cap (e.g., 10x for an equity index
  CFD) doesn't mean trading at the full cap is the normal way to
  trade. The higher the leverage, the faster the margin level can
  drop from even a small price move, so it's common practice to keep
  some buffer rather than using the full amount.
- Treating a 100% margin level as a "safe line": in reality, once the
  level drops below 100% it's already subject to a margin call. To
  keep trading safely, you need to maintain a level comfortably above
  100%.
- Confusing a margin call with a stop-out: a margin call comes with a
  grace period — resolving it in time avoids forced liquidation — but
  a stop-out closes everything instantly, with no grace period. The
  triggering margin level and the room to respond are both different
  between the two.

### What is cash settlement?

> The basic definition of cash settlement ("a trade with no physical
> delivery, where only the price difference between entry and exit
> is settled") was already covered under "What is a CFD?" This
> section builds on that and goes deeper into three angles: when
> P&L is actually locked in, how P&L is calculated across multiple
> trades, and what operations does with settlement itself.

#### When exactly is P&L on a cash-settled trade locked in?

With cash settlement, P&L is locked in at the moment the opposite
trade (a closing order) against your open position is executed.
While a position stays open, its unrealized P&L just fluctuates with
every price move — it isn't yet locked in as anything real.

There are three basic ways to place an order:

- Market order: executes immediately at the current market price
- Limit order: you specify a price more favorable than the current
  one, and the order executes once that price is reached (for a buy, a
  price below the current one; for a sell, a price above it)
- Stop order: you specify a price less favorable than the current one,
  and the order executes once that price is reached (for a buy, a price
  above the current one; for a sell, a price below it)

Any of these can be used both to open a position (an opening order)
and to close one (a closing order).

| | Opening order (opening a position) | Closing order (closing a position) |
|---|---|---|
| **Market** | Opens a new position immediately at the current price | Closes the position immediately at the current price |
| **Limit** | Opens a new position once a specified price more favorable than the current one is reached | Closes the position once a specified price more favorable than the current one is reached |
| **Stop** | Opens a new position once a specified price less favorable than the current one is reached | Closes the position once a specified price less favorable than the current one is reached |

A closing order can either lock in a profit ("take-profit") or lock
in a loss ("stop-loss"). Taking profit means closing at a price more
favorable than the current one, so it uses a limit order; a
stop-loss means closing at a price less favorable than the current
one, so it uses a stop order (either can also be done with a market
order if you want to close right away).

For example, say you open a long (buy) position with a market order
at 100. Closing this position means selling. If you want to lock in
a profit once the price reaches 105, you place a limit sell closing
order (take-profit) at 105. Conversely, if you want to cap your loss
in case the price falls to 90, you place a stop sell closing order
(stop-loss) at 90. If you mistakenly placed a "limit" sell order at
90, it would mean "sell at 90 or higher," and it would execute
immediately at the current 100.

```mermaid
graph LR
    A["Opening order (market)<br/>Open a long position at 100"] --> B{Which way does the price move?}
    B -->|Rises to 105| C["Take-profit line (limit close)<br/>Sell to close at 105 → +5 profit"]
    B -->|Falls to 90| D["Stop-loss line (stop close)<br/>Sell to close at 90 → −10 loss"]
```

Setting the take-profit line with a limit order and the stop-loss
line with a stop order in advance like this lets you lock in P&L
without having to watch the price constantly.

#### A concrete example: how is P&L calculated across multiple trades? (The idea of average execution price)

When you trade the same product multiple times — adding to a
position in stages — it's easiest to think about the P&L of the
whole position in terms of its "average execution price." The
examples below assume the same quantity is traded each time (if the
quantities differ, the average is weighted by quantity).

**Adding to a long position across multiple trades**

| Trade | Execution price |
|---|---|
| 1st (opening) | 100 |
| 2nd (add) | 103 |
| 3rd (add) | 105 |
| 4th (add) | 104 |
| **Average execution price** | (100+103+105+104) ÷ 4 = **103** |

Since the average execution price is 103, closing above 103 produces
a profit, and closing below it produces a loss.

**Adding to a short position across multiple trades**

Say you open a short at 100, expecting the price to fall. Instead,
it rises, so you add to the short at 103. It keeps rising to 105 and
you add there too, then it starts to turn, so you add once more at
104.

| Trade | Execution price |
|---|---|
| 1st (opening) | 100 |
| 2nd (add) | 103 |
| 3rd (add) | 105 |
| 4th (add) | 104 |
| **Average execution price** | (100+103+105+104) ÷ 4 = **103** |

For a short, it works the other way around from a long: closing
below the average execution price produces a profit. Looking only at
the original 100 entry, it might seem like you were sitting on an
unrealized loss once the price ran up to 105 — but measured against
the average execution price (103), the position turns profitable
again once the price falls back below 103.

#### Where do I (in operations) touch the settlement process itself?

- Keeping the client's positions separate from the broker's risk
  management: some brokers let a client hold long and short
  positions in the same product at the same time (the client
  "hedging" their own position, called ryodate in Japanese) and
  close each position individually. In that case, P&L is locked in
  position by position, and P&L matches the average execution price
  only when every position is closed together. The broker's risk
  management, on the other hand, looks at client positions net
  (longs and shorts offset against each other) rather than gross
  (longs and shorts kept separately). However many positions a
  client holds, the broker sees its risk as a single offset position.
- Correcting executions after a rate-feed problem: if the rate feed
  malfunctions, a trade can end up executed at an incorrect price.
  When that happens, operations manually corrects it to the right
  price and notifies the affected client.
- Reconciling settlements: checking that a client's settlement result
  matches both the internal system's records and the cover
  counterparty's (CP) records. This is the settlement-side
  counterpart to the position reconciliation covered later under
  "Long and short."
- Confirming P&L and balance updates: verifying that P&L locked in by
  a close is correctly reflected in the client's account balance.
- Handling slippage: with market orders and stop orders, the actual
  execution price can differ unfavorably from the price seen (or
  specified) when the order was placed (slippage). Operations checks
  whether that gap exceeds the acceptable tolerance and responds if it
  does. Limit orders only execute "at the specified price or better,"
  so unfavorable slippage doesn't occur with them.

#### Where I would have stumbled three years ago

- Treating unrealized P&L as if it were already locked in: no matter
  how large an unrealized gain or loss looks, it's just a mark-to-
  market number until a closing order actually executes. P&L is only
  locked in once that happens.
- Assuming P&L across multiple trades is always determined by a
  single average execution price: if positions are closed one by
  one, the P&L you lock in depends on which position you close. The
  average execution price is a guide to "where the break-even point
  is for the position as a whole." And the fact that the broker
  manages its risk net is a separate matter from how a client's P&L
  gets locked in.
- Assuming a stop-loss placed with a stop order guarantees execution
  at exactly that price: a stop order is an order to "close once the
  specified price is reached," and it doesn't guarantee execution at
  that price. When the market moves sharply, or depending on rate-feed
  conditions, it can execute at a price worse than the one specified
  (slippage).

### Long and short

#### What are long and short, in a nutshell?

Long (buy) and short (sell) describe the "direction" of a trade.

- Holding a long: holding a buy position. You profit if the price
  rises above the price you entered at.
- Holding a short: holding a sell position. You profit if the price
  falls below the price you entered at.

Closing a position is done with a trade in the opposite direction:

- A long is closed with a sell closing order
- A short is closed with a buy closing order

So a long is "enter by buying, finish by selling," and a short is
"enter by selling, finish by buying" — mirror images of each other.

#### Why can a CFD be opened with a sell? (How it differs from the physical asset)

In physical trading, you can't sell something you don't hold. A CFD,
on the other hand, uses cash settlement, so it's a trade where only
the price difference from entry to exit changes hands.

"Opening with a sell" means agreeing to settle, at closing, the
difference between the price you sold at and the price you later
buy back at. If the buy-back price is lower than your sell price, you
receive the difference (a profit); if it's higher, you pay the
difference (a loss).

This is what makes it possible to short-sell without holding the
physical asset. When you short a stock through margin trading, you
borrow the shares from a broker, sell them, and pay a stock
borrowing fee in return (plus a premium charge, called gyaku-hibu,
when the shares are in short supply). With a CFD, the client never
borrows any shares, so none of that is needed.

Think of it as making a promise with a friend about the price of a
game console. You agree: "Let's say I sell it at today's price of
¥1,000, and later I buy it back." If the price has fallen to ¥800 by
the time you buy back, you receive the ¥200 difference. If it has
risen to ¥1,200, you pay the ¥200 difference. Nobody borrows or hands
over the console itself — only the price difference changes hands.

That said, not borrowing shares doesn't mean holding a short costs
nothing. For equity index CFDs that reference futures, the short
side also pays or receives the price adjustment at rollover; for
single-stock and ETF CFDs, it pays or receives rights adjustments and
interest adjustments (see ["Rollover"](./cfd-rollover-and-adjustments.en.md) for details).

#### Stock borrowing and short-selling restrictions

A CFD itself is cash-settled, so looking only at the trade with the
client, there's no need to borrow any physical shares. But the
broker sometimes hedges (covers) the risk from a client's short
position in the actual stock market (more on this under ["The idea
behind cover deals"](./cfd-pricing-and-cover.en.md)). When that hedge requires the broker — or
whoever the broker covers with — to sell the physical stock, they
need to borrow it from somewhere first, just as in margin trading.
This is called securities lending (or, from the borrower's side,
stock borrowing).

How securities lending works:

- An investor holding shares lends them to a broker. In return, the
  lender earns a lending fee, paid as interest (often at a higher
  rate than a bank deposit). While the shares are on loan, the lender
  can still sell them on the market as normal at any time.
- The broker re-lends the shares it collects this way to
  institutional investors or margin traders who want to short-sell,
  earning a fee in the process.

In other words, opening a short in the physical stock market always
requires one extra step: borrowing shares from someone.

When shares can't be borrowed, the broker can no longer hedge in the
physical market. Continuing to accept short positions without being
able to hedge would leave the broker itself carrying directional
risk (a loss if the market moves the wrong way). So for any stock
where shares aren't available to borrow, the broker has no choice
but to restrict new short trades on that product.

This isn't purely up to the broker either — it's also tied to
market-level rules. The typical example is rules that restrict the
price at which a stock that has fallen sharply can be sold short: in
the US, Rule 201 of the SEC's (Securities and Exchange Commission)
Regulation SHO (the "alternative uptick rule"), and in Japan, the
short-selling price restriction (a form of uptick rule). Neither
bans short selling outright; both restrict short sales that would
"pile on" a falling price. It's also tied to any stock-borrowing
restrictions imposed on the broker's own cover counterparty. When
such rules make selling at the cover counterparty difficult, a
broker offering CFDs over the counter restricts new client short
selling accordingly.

#### A concrete example: what happens to P&L, long vs. short, when the price rises or falls?

Say you trade one lot of the Japan 225 CFD at 38,000 (assume one lot
= the index × ¥10; all numbers are illustrative).

| Position | Entry price | Exit price | P&L calculation | Result |
|---|---|---|---|---|
| Long | 38,000 | 38,500 (up) | (38,500 − 38,000) × 10 | ¥5,000 profit |
| Long | 38,000 | 37,500 (down) | (37,500 − 38,000) × 10 | ¥5,000 loss |
| Short | 38,000 | 37,500 (down) | (38,000 − 37,500) × 10 | ¥5,000 profit |
| Short | 38,000 | 38,500 (up) | (38,000 − 38,500) × 10 | ¥5,000 loss |

So a long's P&L is "(exit price − entry price) × trade unit," and a
short's P&L is "(entry price − exit price) × trade unit." When the
price rises, longs gain and shorts lose; when it falls, the reverse
happens — they're always mirror images.

#### Where do I (in operations) track and manage position direction?

Because a CFD is a bilateral (OTC) contract between the broker and
the client, the starting point is understanding the flip: "client
long → broker short," "client short → broker long." Operations
tracks and manages position direction with that relationship in
mind, in a few specific areas:

- Monitoring net position: each product has a defined risk tolerance
  for its net position. Operations watches the market, client limit
  orders, and technical signals to make fast hedging (cover)
  decisions that keep the net position within that tolerance. If it
  looks like it might be exceeded, more cover is added.
- Reconciling positions with cover counterparties: checking that the
  broker's hedge positions match what the PB (prime broker) or LPs
  (liquidity providers) show on their side — looking for any breaks
  (trades that appear on our side but not theirs, or vice versa).
  When a discrepancy turns up, operations contacts the LP to confirm
  rate discrepancies or whether a trade actually executed. This
  reconciliation is done regularly, timed around the most active
  trading hours. Since positions are monitored continuously, a
  slipped execution usually triggers an alert, and each one leads to
  back-and-forth with the LP.
- Monitoring stop-outs and margin levels: for equity indices and
  single stocks, shorts generally tend to run lower margin levels
  than longs, for two main reasons. First, the dividend-equivalent
  adjustment goes to longs and comes out of shorts (for single
  stocks and ETFs, this is paid as a rights adjustment each time a
  dividend goes ex; for equity indices that reference futures, it
  flows through the price adjustment at rollover). However, the price
  adjustment for futures-based equity indices also reflects interest
  rates, so when the effect of interest rates outweighs that of
  dividends (as with US equity indices as of writing), the direction
  flips and the short side receives it. Second, equity indices and
  individual stocks tend to rise over the long run, so for the same
  volatility, shorts are more likely to sit in an unrealized loss
  for extended periods. For commodities such as oil, which side the
  price adjustment works against depends on whether the market is in
  contango or backwardation. On top of that, when the market moves
  sharply in one direction during high volatility, it can burn
  through the margin of clients holding the opposite-direction
  position very quickly. When a client is stopped out, the position
  between that client and the broker disappears, but the cover the
  broker placed against it remains — so the broker's overall
  position can temporarily become lopsided. Orders to adjust that
  cover can also be rejected, so this needs constant monitoring.
- Short-specific regulatory response: when a stock-borrowing
  restriction or a short-selling price restriction (such as the US
  Rule 201) comes into effect, new client short trades on that
  product are halted and a notice is posted on the client trading
  platform. When the restriction is lifted, the lift date is posted
  there as well.
- Reporting: trading volume, client stop-out activity, and related
  data are subject to reporting obligations to regulators and others,
  handled on a regular basis.

#### Where I would have stumbled three years ago

- Assuming short = doing something bad: the word "short-selling" can
  sound like it's working against the market, but in a CFD, short is
  just one of two equally valid trade directions — no different in
  kind from long.
- Assuming that if the client profits, the broker profits too:
  because a CFD is a bilateral contract, when a client is long and
  profiting, the broker is theoretically sitting on the mirror-image
  short with an unrealized loss. (In practice, whatever has been
  covered is offset by P&L on the trade with the cover counterparty,
  but whatever is left uncovered within the risk tolerance flows
  straight into the broker's own P&L. Looking only at the client
  relationship, it's the exact opposite.)
- Picturing a CFD short the same way as "borrowing a stock": from
  the client's side, a CFD is cash-settled, so no shares are actually
  borrowed. Stock borrowing only comes into play when the broker
  hedges in the physical market — that's a separate layer from the
  client's own contract.
- Assuming shorts run lower margin "just because the market is
  going up": there's also a structural factor at play — the
  dividend-equivalent amount paid out by shorts (as a rights
  adjustment for single stocks and ETFs, or through the price
  adjustment for equity indices that reference futures) — so margin
  can erode over time even when the price isn't moving at all. The
  direction of this factor depends on the product and the level of
  interest rates, though: for US equity indices and others where the
  effect of interest rates outweighs that of dividends, it's the long
  side that pays the price adjustment.
