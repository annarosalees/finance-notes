# CFD Notes

🇯🇵 [日本語版](./cfd.md)

### What is a CFD?
A CFD is one type of financial derivative. A derivative is a trade
whose price is derived from (depends on) the price of an underlying
asset. The four main types are:

- Futures: a contract to buy or sell a specific asset at a price
  agreed today, for delivery/settlement on a set future date (e.g.,
  Nikkei 225 futures)
- Options: the right (not the obligation) to buy or sell a specific
  asset at a price agreed today, exercisable on a set future date
- Swaps: an agreement between two parties to exchange different cash
  flows (e.g., interest rates, currencies) over a period
- CFDs (Contracts for Difference): a trade with no physical delivery,
  where only the price difference between entry and exit is settled

So a CFD sits alongside futures, options, and swaps as one of the
four main types of derivatives.

"CFD" stands for "Contract for Difference." In Japanese it's called
差金決済取引 (sakin-kessai torihiki) — literally "difference-
settlement trading."

"Difference settlement" means no physical delivery of the underlying
(a stock, oil, a stock index, etc.) ever happens — only the price
difference from entry to exit changes hands. For example, if you buy
at 100 and sell at 120, you never actually receive 100 worth of the
underlying or hand over 120 worth of it; only the 20 difference is
settled.

FX (foreign exchange trading), something people hear about
constantly, is actually a type of CFD too — you can think of FX as
"a CFD on a currency pair." CFD is the umbrella category, and equity
indices, commodities, and FX all sit inside it.

#### Why can you trade without holding the underlying?
A CFD is built by referencing the price of an underlying asset (a
stock, a commodity, etc.), but it doesn't require the full amount of
capital that buying the underlying outright would. Since a CFD only
settles the price difference, it lets you trade with less capital
(this connects to the idea of leverage, covered in its own section).

Trading the physical underlying also comes with the hassle of
delivery. For something like WTI crude oil, if you keep holding a
futures position past its contract month, physical delivery would
normally be triggered. With a CFD, the broker handles all of that
delivery-related work on the client's behalf, so the client can just
focus on the difference-settlement trade without ever having to
think about the underlying itself.

On top of that, physical trading is only possible while the relevant
exchange is open, whereas CFDs can be traded overnight and on
holidays too.

#### A concrete example: what is a CFD actually referencing?
What a CFD's price actually tracks depends on the product type.

- Japan 225: tracks the price of Nikkei 225 futures as traded on an
  exchange. Which exchange is used as the reference varies by
  broker, but SGX (Singapore Exchange) and CME (Chicago Mercantile
  Exchange) are common examples.
- WTI Crude Oil: similarly, tracks the price of WTI crude oil futures
  traded on an exchange.
- ETF-type CFDs, such as a US semiconductor ETF CFD: tracks the
  price of the ETF itself. A CFD on a US semiconductor ETF, for
  example, tracks the actual price movement of a real ETF like the
  iShares Semiconductor ETF. Note that buying the ETF itself and
  trading a CFD that references it are two different things (see
  Note ① below).
- Products with no exchange involved, like FX or precious metals:
  tracks the spot price, which is set through direct bilateral
  trading between financial institutions rather than on an exchange
  (see Note ② below).

So depending on the product, a CFD is built on top of one of three
types of reference price: futures, an ETF, or a spot rate. The
"difference settlement" mechanism described above is common to all
of them, but what sits behind that mechanism is not uniform — that's
the key point.

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

#### Where does operations (me) fit into a CFD?
Keeping a CFD product running touches many different areas of
operations work. Here's the overall picture; the details of each
area are covered in their own sections (rollover, leverage and
margin, etc.).

- Market and risk management: monitoring market conditions (circuit
  breakers, stock-lending restrictions, etc.), assessing and
  adjusting client position risk, monitoring risk exposure, watching
  for stop-outs (forced liquidation), and checking quoted rates for
  anomalies
- Product operations: handling corporate actions (new listings,
  spin-offs, stock splits, mergers, etc.), tracking exchange
  schedules, determining and applying price adjustment amounts,
  rolling contract months over, and hedging
- Administration and compliance: reconciliation (matching the books
  against actual balances), verifying segregation of client assets,
  preparing reports for regulators (the FSA, the Financial Futures
  Association, etc.), and handling KYC (know your customer) / AML
  (anti-money laundering)
- System operations: incident response, maintaining fallback
  procedures under the business continuity plan (BCP), and
  pre-release testing (UAT) for new products

In short, keeping a single CFD product running requires several
roles working together: getting the price right, managing risk,
staying compliant, and keeping systems running reliably.

#### Where my three-years-ago self would get stuck
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

A CFD's price is always quoted as two values side by side.

- Offer rate (Ask): the price quoted by whoever wants to sell. If
  you're buying, this is the price you buy at.
- Bid rate (Bid): the price quoted by whoever wants to buy. If you're
  selling, this is the price you sell at.

The offer (the seller's asking price) is normally higher than the
bid (the buyer's asking price). The gap between the two is the
"spread," and it's the CFD's real trading cost.

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
- Dividend-equivalent adjustments (for equity index and single-stock
  CFDs): you're not a shareholder, but you still receive an
  adjustment amount equivalent to the dividend when one is paid
  (and pay the equivalent if you're short).
- Trade nearly 24 hours a day, including nights and holidays: not
  limited to exchange hours — many products can be traded overnight,
  including overseas markets.

#### A concrete example: physical WTI crude oil vs. WTI crude oil CFD
To see the difference concretely, compare WTI crude oil futures
(physical) with a WTI crude oil CFD.

| Item | Physical WTI crude oil | WTI crude oil CFD |
|---|---|---|
| Delivery | Physical delivery is triggered when the contract month arrives; avoiding it requires rolling over yourself | No delivery ever happens; the broker handles the rollover on your behalf |
| Capital required | The full trade amount | Margin only (leverage applies) |
| Short selling | Requires borrowing the physical asset first — costly and cumbersome | Can be opened directly as a new short position |
| Trading hours | Limited to the crude oil futures exchange's hours | Often tradable overnight and on holidays |
| Storage / incidental costs | Storage and transport costs can apply | No concept of storage; costs are folded into things like the spread |

So even though the underlying price movement is identical, that one
difference — whether or not you hold the physical asset — cascades
into differences in capital, risk management, and trading
flexibility.

#### Where does operations (me) notice the difference between physical and CFD trading?
Because a CFD never holds the physical asset, it creates operations
work that has no counterpart in physical trading. In practice, this
difference shows up especially in:

- Rollover (rolling the contract month): the rollover process itself
  is unique to CFDs and has no equivalent in physical trading
- Managing the adjustment amount: calculating and applying the
  adjustment that offsets the price discontinuity caused by rollover
- Risk management: because leverage is in play, position risk can
  grow larger than in physical trading, so it needs to be monitored
  and adjusted
- Managing the reference exchange's trading hours: a CFD itself can
  trade overnight and on holidays, but the futures or physical
  exchange it references still has set trading hours, so those hours
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
- Setting spreads: instead of a trading commission like physical
  assets have, managing the CFD-specific cost structure (the gap
  between bid and ask)
- Maintaining the contract-month master data: managing the master
  data for which contract month is referenced until when (the
  foundation that rollover depends on)
- Managing the yen-conversion rate: setting the FX conversion rate
  used when offering an overseas product priced in yen

In short, the defining feature of a CFD — not holding the physical
asset — is exactly what adds these extra management items (price,
risk, timing, units) to the operations side.

#### Where my three-years-ago self would get stuck
"The price moves exactly like the physical asset, so why does a
separate product called a CFD even exist?" — that might be your
first reaction. "Why not just trade the physical asset directly?"

But trading the physical asset directly means you'd have to roll
over the position yourself every time the contract month arrives —
which is a hassle, and if you got it wrong, you could actually end
up with the physical asset (crude oil or some other commodity)
delivered to you. A CFD exists precisely because the broker takes on
that hassle and delivery risk on your behalf.

That said, this doesn't mean "a CFD is simply the better deal." A
CFD carries its own cost — the spread (the gap between bid and ask)
— and because leverage is in play, unrealized losses can grow faster
than they would with the physical asset. "No delivery, so it's
convenient" and "lower risk" are two different things, and using a
CFD means understanding its specific costs and risks too.

### What is a rollover?
A rollover involves two things happening together:
1. Rollover (contract rollover): When a futures contract reaches its
   contract month, delivery (settlement) becomes due. So the position
   is closed out and re-opened under a new contract month.
2. Reference month shift: The price reference moves from the near
   month to the far month.

A CFD itself has no expiry, but the futures contract it's based on
does — so a rollover is needed to keep the CFD running. The contract
month used as the reference is always the one with the highest
trading volume.

### Why does a rollover happen?
Futures contracts have a "contract month" — a promise for when and
at what price the underlying will be delivered in the future. When
that date arrives, delivery (settlement) is triggered. A CFD,
however, is cash-settled (no physical delivery), so before the
contract month's delivery date arrives, the position rolls over into
the next contract month. This happens shortly before the delivery
date — not on the day itself — and the exact timing varies by
product.

### What happens to the rate and position at rollover?
Whenever the "front month" (the contract month with the highest
trading volume at a given time) changes on the exchange, the
reference contract month rolls over to the next one. This is what
lets a CFD keep running indefinitely without ever expiring.

The moment the reference month changes, though, the price jumps
discontinuously — and so does the unrealized P&L on any open
position. To offset this, an adjustment amount is credited or
debited in the opposite direction of that P&L jump, so the rollover
itself leaves the client neither better nor worse off:

- Price rises at rollover → longs gain, so the adjustment is
  negative; shorts lose, so the adjustment is positive
- Price falls at rollover → longs lose, so the adjustment is
  positive; shorts gain, so the adjustment is negative

This adjustment amount is made up of two components:
1. **Interest adjustment** — a short-term interest equivalent for
   the time remaining to settlement. It reflects the interest-rate
   gap between holding the spot asset and holding a futures
   position, and it's baked into the futures price for every
   product type (indices, FX, metals, energy, commodities, etc.).
2. **Dividend adjustment** — the present value of expected future
   dividends. Since a company's value (and so its share price)
   drops by roughly the dividend amount when it's paid out, futures
   prices are set lower in advance to account for it. This only
   applies to equity indices — not to FX, metals, or energy, which
   pay no dividends.

The further out a contract month is, the more dividend payments
fall within its remaining life, so it trades at a correspondingly
lower price (for indices). As settlement approaches, the interest
component shrinks and the price converges toward the dividend-
adjusted level — ending up close to the spot price.

The adjustment is calculated as:
`(near-month mid − far-month mid) × contract size × FX conversion rate`

It's applied on the same day as the rollover, after that day's
trading closes.

### What does the operations side do at that point?
On a rollover day, operations handles four main tasks:
1. **Scheduling** — pull the rollover schedule from the data
   provider, confirm the dates, register them in the system, and
   publish the schedule to clients.
2. **Rolling the reference contract month** — verify the far
   month's price settings are correct, and confirm the switch to
   the new reference month is complete on the day itself.
3. **Settling the adjustment amount** — the system applies the
   adjustment to client accounts automatically, but since a wrong
   figure directly affects client P&L, checking it beforehand is
   critical.
4. **Rolling the cover position** — the firm's own hedging position
   (the other side of client positions) must also be closed and
   re-opened in the far month before settlement, and this needs to
   be confirmed as done *before* the adjustment day — unlike task 2,
   which is confirmed *on* the day itself.

### Summary
These pieces all trace back to a single thread: because the futures
contract behind a CFD always has an expiry and a contract month, the
CFD has to roll over to keep running without interruption. Rolling
over always creates a price discontinuity, which the adjustment
amount exists to offset — and that adjustment amount is itself built
from interest rates and (for some products) dividends, the very
things that shape the futures price in the first place. Rollover,
the adjustment, and interest/dividends aren't separate topics — they
all fall out of one fact: futures contracts expire.
