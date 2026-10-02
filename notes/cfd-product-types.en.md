# CFD Notes: Examples by Product Type

🇯🇵 [日本語版](./cfd-product-types.md)

[← Back to the CFD notes index](./cfd.en.md)

This file lays out the differences between product types such as
indices, commodities, US stocks, and ETFs, organized around what each
CFD references.

---

### Examples by Product Type (Indices / Commodities / US Stocks & ETFs)

The sections so far have used Japan 225 and WTI crude oil as examples
to explain the mechanics common to all CFDs. This section changes the
angle and lines product types up side by side to see "what's
different."

#### Index, commodity, and US stock/ETF CFDs — what's the difference, in a nutshell?

The starting point for every difference is "what the CFD's rate
references" (its reference). For the reference itself, see the
concrete example under ["What is a CFD?"](./cfd-basics.en.md). A
different reference changes whether rollover happens and what you need
to watch out for.

| Product type | Reference | Currency examples | Rollover | Key things to watch |
|---|---|---|---|---|
| Index (e.g., Japan 225) | Exchange-traded futures | JPY (Japan 225), EUR (DAX), HKD (Hang Seng) | Yes | Some brokers offer indices with no contract month |
| Commodity (e.g., WTI crude oil) | Exchange-traded futures | USD | Yes | Units |
| Spot precious metals (e.g., spot gold) | USD-denominated spot trading | USD | No contract-month rollover (the value date is rolled forward daily) | Same mechanics as FX |
| US stocks & ETFs | The listed stock or ETF itself | USD | No | Corporate actions, trading hours, short restrictions |

- Index CFDs: they reference exchange-traded futures, so a rollover
  happens whenever the futures contract month (the month in which
  the contract expires) changes. Some brokers, however, offer index
  CFDs that reference the index itself (the cash index) rather than
  futures, with no contract month. In that case there's no rollover;
  instead, the gap to futures is bridged by adjustments for interest
  and dividend-equivalents over the holding period.
  The index itself is only calculated while the reference exchange
  is open, so outside those hours many brokers build the price from
  futures movements and similar inputs.
  <!-- To confirm: how cash-index CFDs without a contract month are priced while the exchange is closed -->
- Commodity CFDs: like indices, they reference exchange-traded
  futures, so a rollover happens. Precious metals, though, differ in
  character depending on the reference even within "commodities."
  Products that reference spot trading, like spot gold, work the
  same way as FX (covered in detail under "Do rollover and
  adjustments work differently by product type?" below). Precious
  metals that reference futures roll over normally, like any other
  commodity.
  Commodities also call for special attention to units. What the
  price is "per" differs by product: WTI crude is quoted in dollars
  per barrel (about 159 liters), and gold in dollars per troy ounce
  (a unit of weight used for precious metals, about 31.1 grams). Some
  futures, like corn and soybeans, are even quoted in cents rather
  than dollars.
  On top of that, the trade unit (quantity per lot) of the exchange
  futures used for cover and that of the CFD often don't match. WTI
  crude futures, for example, trade on the exchange in large units
  of 1,000 barrels per contract, while a broker may set a much
  smaller CFD trade unit so retail clients can trade more easily. In
  that case, client CFD volume can't be mapped one-to-one onto
  futures contracts, and cover trades require converting "how many
  CFD units equal one futures contract" (for cover trades themselves,
  see ["The Idea Behind Cover Deals"](./cfd-pricing-and-cover.en.md)).
- US stock & ETF CFDs: they reference the listed stock or ETF itself.
  There's no rollover since they aren't futures, but you need to
  watch the following:
  - Corporate actions (CA): events initiated by the company — stock
    splits, reverse splits, spin-offs, dividends — that change the
    share price or share count. When they happen, the CFD side needs
    to respond too (covered in ["When a Spin-off, Reverse Split, or
    Stock Split Happens"](./cfd-rollover-and-adjustments.en.md) and ["When a Dividend Is Paid
    (Rights Adjustment)"](./cfd-rollover-and-adjustments.en.md)).
  - Trading hours: they follow US exchange hours, which means
    overnight trading in Japan time. Regular trading hours are 23:30
    to 6:00 the next morning Japan time, moving an hour earlier to
    22:30 to 5:00 during US daylight saving time. Depending on the
    broker, you may also be able to trade during extended hours
    before and after the regular session (pre-market and
    after-market).
    Trading hours can also change along with the reference market.
    In the US, for example, Nasdaq plans to start 23-hour trading on
    December 6, 2026 (US Eastern Time; as of writing), and CFD trading
    hours may be extended along with it.
  - Short restrictions: for single stocks, opening a short can be
    restricted depending on stock borrowing conditions (see the stock
    borrowing part of ["Long and Short"](./cfd-basics.en.md)).
- ETF CFDs: like single stocks, ETF CFDs reference the listed ETF
  itself, so there's no rollover; instead there are rights
  adjustments (adjustments for dividends and other shareholder
  rights; for ETFs, distribution-equivalents) and interest
  adjustments. The leverage cap is also the same as for single
  stocks. ETFs do have some differences of their own, though.
  Take a US semiconductor ETF (e.g., the iShares Semiconductor ETF).
  It's built to track a stock index of US semiconductor-related
  companies, so it moves as if you held a basket of several
  semiconductor companies' shares.
  - Diversification means one company's news matters less than for a
    single stock: a single earnings release is less likely to make the
    price jump the way it would for an individual stock. That said,
    an ETF focused on one sector, like semiconductors, can still move
    sharply on the earnings of heavily weighted companies or on
    industry-wide news, so it isn't necessarily as calm as a broad
    equity index.
  - Distribution frequency varies by ETF: some pay monthly, some
    quarterly (four times a year), and so on. The timing of rights
    adjustments therefore needs to be checked per product.
  - ETFs can be terminated: the fund manager can decide to wind an
    ETF down (redemption). When that happens, the reference
    disappears, so CFD positions need to be closed out or otherwise
    handled.
  - Some ETFs hold futures: some ETFs that track oil and similar
    products actually run by holding oil futures. In that case, even
    though the CFD itself has no rollover or price adjustment, the ETF
    rolls futures internally, and contango gradually shows up in the
    ETF's own price. "It references an ETF, so rollover doesn't
    matter" isn't always true.
  - Leveraged ETFs exist too: for example, there are ETFs designed to
    move three times as much as semiconductor stocks. Because they
    reset every day to "three times that day's move," holding one for
    a long time doesn't give you exactly three times the underlying
    index's move — it drifts away from that.

A caution that cuts across product types is currency. Currency
depends not on the product type but on the reference market (a CFD's
currency is basically set by the broker to match the reference
market's currency). Even among indices, Japan 225 is in yen, DAX and
Euro Stoxx 50 in euros, and the Hang Seng in Hong Kong dollars. For
products denominated in a currency other than yen, P&L is first
calculated in that currency and then converted into yen before it
hits the account. So on top of the price movement of the product
itself, you're also exposed to the exchange rate used for conversion
(e.g., USD/JPY or EUR/JPY).

Conversion into yen generally works like this:

- Unrealized P&L on open positions: converted into yen at the
  exchange rate of the moment for display. So even if the product's
  rate doesn't move, yen-based unrealized P&L changes when the
  exchange rate moves.
- P&L on closing a position: converted into yen and locked in at the
  exchange rate at the time of closing.
- Adjustments (price adjustment amounts, rights adjustments, and
  interest adjustments): generally calculated at the mark-to-market
  point after each day's trading, converted into yen at the FX
  conversion rate at that time, and applied to the account (see
  "When and at what price are adjustments calculated?" below).

The detailed rules for which exchange rate is used and when vary by
broker.

**Other product types**

Beyond the indices, commodities, US stocks, and ETFs covered here,
CFDs come in many other product types. Two representative ones are
bonds and VIX. For both, thinking in terms of the reference, the same
framework applies to whether there's a rollover and which adjustments
apply (although what creates the futures price gap differs by
product).

- Bond CFDs: CFDs that reference government bond futures prices
  (e.g., US 10-year Treasury note futures). Bond prices move opposite
  to interest rates — when rates rise, prices fall, and when rates
  fall, prices rise. That's because bonds already issued carry a
  fixed rate, so when market rates rise they become relatively less
  attractive and their price drops. Since they reference futures,
  they roll over and carry price adjustments just like indices and
  commodities. Because their price moves are relatively calm, the
  leverage cap for retail CFDs in Japan is set at 50x (as of writing),
  higher than other product types.
- VIX CFDs: VIX, also called the "fear index," is a number
  expressing how much investors expect a major US stock index (the
  S&P 500) to move over the next 30 days. It spikes when anxiety
  spreads through the market and falls when things calm down. VIX
  itself is a calculated number and can't be traded directly, so the
  CFD references VIX futures.
  VIX futures have a contract every month and in normal times tend to
  be in steep contango. VIX tends to drift back toward its normal
  level over time even after a spike, so compared with a low VIX in
  calm periods, contracts further out tend to be priced higher, closer
  to the longer-run average level. A risk premium — extra paid as
  protection against volatility rising in the future — is also cited
  as a reason. This is where VIX futures differ from equity index or
  crude oil futures, whose price gaps are set by interest, dividends,
  and storage costs. Holding a long therefore tends to pile up price
  adjustment payments with each rollover. And just as with Japan 225,
  the VIX number you see in the news doesn't match the VIX CFD rate.

---
Note: the same "Japan 225" isn't always in the same currency

Nikkei 225 futures are listed on several exchanges, and even though
they track the same index, they aren't necessarily in yen. CME
(Chicago Mercantile Exchange), for example, lists both a yen-
denominated and a dollar-denominated Nikkei 225 futures contract.
Both track the same Nikkei Stock Average and move almost identically,
but P&L is calculated in yen for one and in dollars for the other.

In other words, "same product name" doesn't guarantee "same
currency." A CFD's currency is basically set by the broker to match
the reference market's currency, so it's important to check which
exchange's contract, in which currency, the CFD references.

#### Do rollover and adjustments work differently by product type?

Whether a rollover happens, and which adjustments apply, differ by
product type. As in the previous subsection, those differences also
come from the reference.

| Reference | Product types | Contract-month rollover | Adjustments | When they occur |
|---|---|---|---|---|
| Futures | Indices (e.g., Japan 225), commodities (e.g., WTI crude, precious-metal futures) | Yes | Price adjustment amount | Price adjustment day (at rollover) |
| Single stock / ETF | US stocks, ETFs | No | Rights adjustment, interest adjustment | Rights adjustment: ex-dividend date (the day the right to the dividend drops off) / Interest adjustment: according to the number of days the position is carried |
| Spot | Spot precious metals (e.g., spot gold) | No (but the value date is rolled forward daily) | Interest adjustment | According to the number of days the position is carried |

- Products referencing futures: before the referenced futures
  contract expires, the position rolls to the next contract month.
  A price adjustment amount is applied to bridge the price gap that
  appears at the moment of rollover (see ["What is a
  rollover?"](./cfd-rollover-and-adjustments.en.md)).
- Products referencing single stocks or ETFs: there's no contract
  month, so no rollover. Instead, rights adjustments (dividend
  equivalents) and interest adjustments apply. ETFs pay
  distributions rather than dividends, but CFDs treat them the same
  as a single stock's dividend — as a rights adjustment.
- Products referencing spot precious metals (e.g., spot gold): with
  no contract month, there's no futures-style rollover. That doesn't
  mean delivery never comes into play, though. Spot trades settle
  (deliver) two business days after the trade. To avoid delivery,
  the CFD rolls the value date forward every time the position is
  carried to the next day (the same mechanism as FX swap points).
  Interest-equivalent amounts arise from this rolling forward, and
  are paid or received as the interest adjustment.
  Precious metals that reference futures, on the other hand, are
  handled like "products referencing futures" above, with a normal
  rollover and price adjustment amount. In other words, what decides
  the treatment isn't "is it a precious metal?" but "is the reference
  spot or futures?"

**Direction of payment**

How the direction of payment is decided depends on the type of
adjustment.

- Price adjustment amount: decided by whether the price rose or fell
  at rollover. That direction is tied to what's inside the price gap
  (interest, dividends, storage costs, supply and demand) — see
  ["What is a rollover?"](./cfd-rollover-and-adjustments.en.md).
- Rights adjustment: longs receive, shorts pay (for the dates involved
  and the full mechanism, see ["When a Dividend Is Paid (Rights
  Adjustment)"](./cfd-rollover-and-adjustments.en.md)).
  A long moves the same way as someone holding the stock, so like a
  shareholder it receives the dividend. A short is in the same
  position as someone who borrowed the stock and sold it; that
  person has to pay the dividend to the lender when one is paid, so
  a CFD short pays the dividend-equivalent too (for how stock
  borrowing works, see ["Long and Short"](./cfd-basics.en.md)).
  Depending on the tax rules of the country where the stock is
  listed, dividends may or may not be subject to withholding tax
  (tax deducted at the time of payment). Where withholding applies,
  the long receives the after-tax amount, which may not equal what
  the short pays.
- Interest adjustment: depending on conditions, it can be either a
  receipt or a payment. It isn't always "longs pay, shorts receive."
  The reasons:
  - The base interest rate itself can go negative (as in past periods
    of negative rates for the euro and the yen).
  - Some products, like spot gold, are driven by the difference
    between two interest rates (the same idea as FX swap points; see
    the FX notes).
  - The rates applied to longs and shorts include a spread for the
    broker's fee, so in some conditions both longs and shorts end up
    paying.

**When and at what price are adjustments calculated?**

Adjustments aren't calculated trade by trade in real time. They're
generally calculated and applied in bulk during the daily process
after each day's trading ends (mark-to-market and settlement
processing). Mark-to-market means revaluing held positions at that
day's reference price (the settlement price) as a daily process.

There are two reasons to calculate them in bulk in the daily process:

1. To apply the same basis to every client: calculating with the
   same day's prices and exchange rates at the same moment means no
   client is advantaged or disadvantaged.
2. To lock in positions before calculating: calculating after all of
   the day's trading has finished means "who carried how many lots
   into the next day" is settled. Both interest and rights
   adjustments apply to "whoever held the position at that point,"
   so positions need to be locked in at the day boundary.

The price used in the calculation, and the exchange rate used to
convert into yen, differ by type of adjustment:

| Adjustment | Price used | Exchange rate for yen conversion |
|---|---|---|
| Interest adjustment | Based on position value (settlement price used for mark-to-market × quantity) | FX conversion rate at mark-to-market |
| Rights adjustment | Dividend per share (the announced, confirmed figure) × number of shares; no price is used | FX conversion rate at mark-to-market on the day it's applied |
| Price adjustment amount | The near/far month price gap on the price adjustment day | FX conversion rate on the price adjustment day |

Only for the price adjustment amount does the price used differ by
broker:

- Brokers that use the exchange's official settlement prices (for
  the near and far months respectively)
- Brokers that use the mid (halfway between bid and ask) at a set
  time after trading closes

Either way, what matters is comparing the near and far months at
the same moment. If the timing is off, the price movement in between
gets mixed into the gap, and the price discontinuity from rollover
can't be offset correctly.

**Same words — "interest adjustment" and "rights adjustment" — different roles**

What's easy to get confused about here is that the words "interest
adjustment" and "rights adjustment" also appeared in the
["rollover"](./cfd-rollover-and-adjustments.en.md) section. The words
are the same, but their role differs between products that reference
futures and products that don't.

The difference comes down to whether the referenced price is "a
future price" or "today's price."

- A futures price is "the price for a future delivery date," so
  interest until that date and the expected dividends in between are
  built into the price from the start. CFDs referencing futures
  therefore don't need to pay or receive interest and dividends
  separately; they're settled together inside the price gap at
  rollover (the price adjustment amount).
- The price of a single stock or spot product is "today's price," so
  interest and dividends over the holding period aren't included in
  it. Interest for the holding period, and a dividend-equivalent when
  a dividend is paid, need to be paid or received separately from
  the price.

| | Products referencing futures (indices, commodities) | Single stocks, ETFs, spot precious metals |
|---|---|---|
| What "interest adjustment" and "rights adjustment" mean | Ingredients built into the futures price | Adjustments paid or received directly in the client's account |
| What the client actually pays or receives | The price adjustment amount (all at once, at rollover) | Interest and rights adjustments (each time they occur) |
| When a dividend is paid | Nothing is paid or received at that moment (expected dividends are already priced into futures) | A rights adjustment is paid or received on the ex-dividend date |

So the purpose — settling up for interest and dividends — is the
same, but futures do it "inside the price, all at once at rollover,"
while single stocks and spot products do it "separately from the
price, each time."

**How the price adjustment day is chosen also differs by product**

Even among products referencing futures, how the price adjustment
day (the day of rollover) is chosen differs by product. The basic
idea is to use "the day when liquidity in the near month (the
contract closest to expiry) and the far month (the one further out)
is just about to flip" as the benchmark. Rolling over when the
center of trading moves to the far month keeps the reference price
from drifting away from where the real trading is.

| Product | Typical price adjustment day | Why |
|---|---|---|
| Equity indices (e.g., Japan 225) | Just before SQ (the Special Quotation date / final settlement of the futures) | Just before SQ is standard for equity indices |
| Crude oil (e.g., WTI crude) | Before the last trading day (how many business days before varies by broker) | As the last trading day approaches, near-month trading thins out and the center of trading moves to the far month, so the rollover follows that shift |
| Grains such as corn and soybeans | Well before the last trading day | Near-month liquidity drops off well before the last trading day, so the rollover is moved earlier accordingly |

#### A concrete example: Japan 225, WTI crude oil, spot gold, and US stock CFDs side by side

Here's everything so far, lined up for representative products.

| | Japan 225 | WTI crude oil | Spot gold | US stocks (single stock) |
|---|---|---|---|---|
| Product type | Index | Commodity | Commodity (precious metal) | Equity |
| Reference | Exchange-traded Nikkei 225 futures | Exchange-traded WTI crude futures | USD-denominated spot trading | The single stock listed on a US exchange |
| Currency | JPY | USD | USD | USD |
| Price unit | Index points | USD per barrel | USD per troy ounce | USD per share |
| Trade unit caveat | The futures trade unit and the CFD trade unit may differ | Futures are 1,000 barrels per contract; the CFD may use a smaller unit | ― | ― |
| Trading hours (Japan time) | Nearly 24 hours on weekdays (depends on broker and reference) | Nearly 24 hours on weekdays (depends on broker and reference) | Nearly 24 hours on weekdays (like FX) | Regular hours 23:30–6:00 (22:30–5:00 in daylight saving time); some brokers also offer pre/after-market (*) |
| Contract-month rollover | Yes | Yes | No (value date rolled forward daily) | No |
| Rollover frequency | Four times a year (March/June/September/December contracts) | Every month | ― | ― |
| Adjustments | Price adjustment amount | Price adjustment amount | Interest adjustment | Rights adjustment, interest adjustment |
| When adjustments occur | Price adjustment day | Price adjustment day | According to days carried | Rights adjustment: ex-dividend date / Interest adjustment: according to days carried |
| Dividend treatment | Expected dividends priced into futures (settled via the price adjustment amount) | No dividends | No dividends | Paid or received as a rights adjustment on the ex-dividend date |
| Long-side adjustment tendency | Tends to receive when the dividend effect outweighs interest (as of writing) | Pays in contango, receives in backwardation | Depends on conditions | Receives the rights adjustment (after tax where withholding applies); interest adjustment depends on conditions |
| FX exposure | None | Yes (USD/JPY) | Yes (USD/JPY) | Yes (USD/JPY) |
| Key things to watch | Some brokers offer indices with no contract month | Units; longs pay at every rollover while contango persists | Precious metals that reference futures do roll over | Corporate actions, short restrictions, changes to trading hours |

(*) US exchanges are moving to extend trading hours: Nasdaq plans to
start 23-hour trading on December 6, 2026 (US Eastern Time; as of
writing). CFD trading hours for US stocks and related indices may be
extended accordingly. Trading hours aren't fixed — they can change
along with the reference market.
<!-- To confirm: after 23-hour trading starts, check the actual start date, covered products, and changes to CFD trading hours, and update -->

**What happens if you hold a long for one month?**

Let's see how the differences in the table actually show up when
you hold a position. Assume the following:

- You hold 1 lot of each of the four products, long, for one month.
- The CFD rate (the price shown on screen) is at the same level at
  the start and end of the month — so P&L from price movement is
  zero.
- The month is a Nikkei 225 futures contract month (March, June,
  September, or December).

With P&L from price movement set to zero, only the differences by
product type (adjustments and FX) remain.

| | Japan 225 | WTI crude oil | Spot gold | US stocks (single stock) |
|---|---|---|---|---|
| What happens during the month | One price adjustment day | One price adjustment day | Interest adjustment every day | Interest adjustment every day; rights adjustment if there's an ex-dividend date |
| Long-side direction | Tends to receive (as of writing) | Pays in contango | Depends on conditions | Receives the rights adjustment; interest adjustment depends on conditions |
| FX exposure | None | Yes | Yes | Yes |

- Japan 225: since it's a contract month, the price adjustment day
  falls mid-month. In the same situation as the rollover section's
  worked example (near ¥38,000, far ¥37,900), a client long 1 lot
  receives a +¥1,000 price adjustment amount.
  At the moment of rollover, the rate drops ¥100 and unrealized P&L
  falls ¥1,000, which the +¥1,000 adjustment makes up, so the net is
  zero. But when the rate returns to the start-of-month level by
  month-end, unrealized P&L recovers and only the +¥1,000 received
  remains. That's what "longs tend to receive" actually looks like.
  In a non-contract month, nothing happens over a month of holding.
  Japan 225 only rolls four times a year, so what happens depends on
  the month.
- WTI crude oil: there's a contract every month, so any month you
  hold it you'll hit one price adjustment day. In the same situation
  as the rollover section's worked example (near $70.00, far $70.50,
  contango), a client long 1 lot pays ¥750. The opposite of Japan
  225: when the rate returns to the start-of-month level by
  month-end, the ¥750 paid remains as a loss. This repeating every
  month is what "holding a long for a long time on a product that
  stays in contango piles up payments" means.
- Spot gold: with no contract month there's no rollover, but the
  interest adjustment moves each time the position is carried
  overnight. Accumulating a little every day over the month — rather
  than moving all at once monthly like Japan 225 and WTI crude — is
  the difference. The interest adjustment is calculated as:
  position value (settlement price used for mark-to-market ×
  quantity) × annual interest rate × days ÷ 365 (or 360)
  For spot gold, the "annual interest rate" is the difference between
  the US dollar interest rate and the rate for lending and borrowing
  gold (the lease rate) — the same idea as FX swap points.
  When the carry spans a weekend or holiday, those days are counted
  together. Which day of the week picks up the weekend depends on how
  the value date is counted. For spot trades that settle two business
  days after the trade, like spot gold, the three days are usually
  applied on a Wednesday carry, when the value date spans the
  weekend, just as in FX (this varies by broker). Whether it's a
  receipt or a payment depends on interest-rate conditions at the
  time.
- US stocks: like spot gold, the interest adjustment moves every day
  (same formula; the annual rate is the US dollar rate adjusted up or
  down by the broker's fee, and the weekend is charged as three days
  on a Friday carry). On top of that, if a stock you hold goes
  ex-dividend that month, you receive a rights adjustment. Many US
  stocks pay dividends four times a year, so an ex-dividend date
  typically comes around once every three months. The rights
  adjustment is calculated as:
  dividend per share × shares held
  Where withholding tax applies, the long receives the after-tax
  amount.

In addition, the three products other than Japan 225 are
USD-denominated, so if USD/JPY moves during the month, yen-converted
P&L changes too. Even with the rate at the same level as at the
start of the month, a stronger yen shrinks the yen value and a
weaker yen increases it.

This example looked at holding long positions; holding short
positions flips every direction. The Japan 225 price adjustment
amount is paid by shorts, shorts receive in WTI crude contango, and
shorts pay the US stock rights adjustment.

To sum up, even in the same situation — "held long for a month, and
the rate didn't change":

- Japan 225 receives in a contract month (when the dividend effect
  outweighs interest, as of writing), and nothing happens otherwise
- WTI crude always has a payment or receipt every month, paying in
  contango
- Spot gold and US stocks have small payments or receipts every day,
  with US stocks getting a lump receipt on ex-dividend dates
- The three USD-denominated products are also exposed to FX

What happens in the account is completely different. That's what
"differences by product type," born from differences in reference,
actually look like.

#### Do I (in operations) handle things differently depending on product type?

Most operations work is common across product types (for the
overall picture, see "Where do I (in operations) notice the
difference between physical and CFD trading?" under ["Why does a CFD
exist as a product?"](./cfd-basics.en.md)). But as we've seen, a
different reference means different things happen, so there are many
situations where the response changes by product type. Here too,
they're organized by reference.

**Products referencing futures (indices, commodities)**

- Setting the price adjustment day: the benchmark for the price
  adjustment day differs by product (just before SQ for equity
  indices, before the last trading day for crude oil, well before the
  last trading day for grains, and so on — see "How the price
  adjustment day is chosen also differs by product"). When starting
  to handle a new product, the principle for its price adjustment day
  has to be set by looking at when liquidity flips between its near
  and far months (for the overall flow of adding a product, see
  ["Adding a New CFD Product in Practice"](./cfd-product-listing.en.md)).
- Rolling cover positions, and differences in how the reference
  settles: how futures settle at expiry differs by product. Nikkei
  225 futures are simply cash-settled at expiry (SQ), with no
  physical delivery. WTI crude futures, on the other hand, trigger
  actual delivery of crude oil if held to expiry. So for products
  with physical delivery like WTI crude, reliably finishing the cover
  rollover ahead of expiry matters even more — if it's late, the
  broker takes on the obligation to receive (or deliver) actual
  crude.
- Converting trade units: commodities in particular can have very
  different trade units between the exchange futures and the CFD
  (e.g., WTI crude futures are 1,000 barrels per contract). When
  deciding cover quantities, you have to convert how many CFD units
  equal one futures contract.

**Products referencing single stocks or ETFs**

- Checking and registering rights adjustments: check dividend
  announcements (distributions for ETFs) on a data terminal or
  similar, and register them in the system by the ex-dividend date.
  A registration error directly affects client accounts, so checking
  beforehand is especially important. When the start of handling a
  new product coincides with an ex-dividend date, you need to prepare
  in advance so the first rights adjustment is registered in time.
- Checking withholding tax: whether dividends are subject to
  withholding tax, and at what rate, depends on the country where the
  stock is listed. When starting to handle products from a new
  country, withholding treatment needs to be confirmed with tax
  specialists in advance.
- Registering interest adjustment day counts: the day counts used to
  calculate interest adjustments (the days counted together when a
  carry spans a weekend or holiday) are registered in the system in
  advance. The same applies to products referencing spot trading,
  such as spot gold, with day counts set to match how the value date
  is counted.
- Corporate actions: when a split, reverse split, spin-off, or
  similar happens, CFD positions and prices need to be adjusted
  (covered in ["When a Spin-off, Reverse Split, or Stock Split
  Happens"](./cfd-rollover-and-adjustments.en.md)).
- Checking stock borrowing and short-selling restrictions: for single
  stocks, stock borrowing conditions or short-selling restrictions
  can make it necessary to restrict new shorts (see ["Long and
  Short"](./cfd-basics.en.md)).
- Monitoring single-stock events: single stocks can move sharply
  outside trading hours, for example on earnings. The next session
  then opens with the price jumping away from the prior close (a
  gap), which tends to knock some clients' margin levels down at
  once. And when trading in a stock is halted or it's delisted, the
  broker also has to decide how to handle CFD positions (halting
  trading, forced liquidation, etc.).

**Products referencing spot (spot gold, etc.) and single stocks/ETFs**

- Checking the direction of interest adjustments: interest
  adjustments can be a receipt or a payment depending on rates. So,
  as a practitioner, I check that the direction hasn't flipped and
  that the configured rates match actual rate conditions.

**Things that change with the reference market (common to all product types)**

- Leverage caps and margin rates: for retail CFDs in Japan, the
  leverage cap differs by product type (as of writing, 10x for equity
  indices, 20x for commodities, 5x for single stocks and ETFs, etc. —
  see ["Leverage and Margin"](./cfd-basics.en.md)). Margin-rate
  settings and margin-level monitoring also follow each product type's
  standards.
- Different market holidays: each reference market has its own
  holidays (Japanese holidays, US holidays, etc.). How to handle CFD
  rate distribution and trading on days the reference is closed, and
  how to count interest adjustment days across holidays, need to be
  checked per product.
- Different price-limit and trading-halt mechanisms: the mechanisms
  that stop trading in a sudden market move differ by reference.
  Futures have exchange-set price limits and circuit breakers
  (rules that temporarily halt trading after moves beyond a set
  size). US stocks have mechanisms that briefly halt trading in a
  single stock when it moves beyond a set band, and market-wide
  circuit breakers that halt all stocks in a sharp market drop.
  OTC products like spot gold, by contrast, have no exchange-style
  limits. So the criteria for deciding when to stop CFD rate
  distribution or cover because of something at the reference also
  differ by product type.
- Daylight saving time and trading-hour changes: products that
  reference overseas markets need their trading hours changed when
  daylight saving time switches. And when the reference market
  changes its trading hours altogether, like the US move to 23-hour
  trading, the CFD's trading hours need to be revisited too.
- Managing the FX conversion rate: products in currencies other than
  yen, such as USD, need the exchange rate used to convert P&L into
  yen (the FX conversion rate) to be managed. It isn't needed for the
  yen-denominated Japan 225.
- Calculating market risk: the method for calculating market risk
  under capital adequacy rules also differs by product type
  (equities, including equity indices; gold; and other commodities
  are each calculated differently — see ["Position Limits and Cover
  Strategy"](./cfd-pricing-and-cover.en.md)).

#### Where I would have stumbled three years ago

Assuming "the Japan 225 rate = the Nikkei Stock Average itself"

The Nikkei Stock Average you see in the news and the Japan 225 CFD
rate are not the same number. That's because what the Japan 225 CFD
references is not the Nikkei Stock Average itself (the index) but the
price of Nikkei 225 futures.

Futures prices have interest and expected dividends until the
delivery date built in (see ["What is a
rollover?"](./cfd-rollover-and-adjustments.en.md)). So the futures
price doesn't match the index itself. For Nikkei 225 futures, as of
writing, the dividend effect outweighs interest, so futures often
trade slightly below the index. The gap narrows as SQ (the final
settlement of the futures) approaches, and widens again when the
reference switches to the far month at rollover.

Also, the Nikkei Stock Average is only calculated while the Tokyo
Stock Exchange is open, but Nikkei 225 futures trade overnight too.
That's why the Japan 225 CFD moves during the Japanese night — the
news Nikkei is frozen in the middle of the night, yet the CFD rate is
moving.

Furthermore, Nikkei 225 futures aren't listed on just one exchange —
they're listed on several, including Osaka Exchange, SGX (Singapore
Exchange), and CME (Chicago Mercantile Exchange), each with different
trading hours. Because a CFD isn't exchange-traded but an OTC product
where the broker chooses the reference to build its rate, it can
switch which exchange it references depending on the time of day.
When one exchange is closed, referencing futures trading on another
lets the CFD offer nearly 24-hour weekday trading without being tied
to any single exchange's hours. Exchange-traded futures also have
night sessions, but combining futures from several exchanges by time
of day into a single rate is something only an OTC CFD can do.

That said, being able to trade 24 hours doesn't mean conditions are
the same at all hours. How active trading is at the reference
(liquidity) varies greatly by time of day, and the lower the
liquidity, the wider the spread (the gap between bid and ask) tends
to be. For Japan 225, trading is active during Tokyo hours and during
US hours, but tends to thin out in between.
Liquidity also differs by product type. Generally, major equity
indices like Japan 225 and major commodities like WTI crude are
highly liquid with tight spreads, while single stocks — especially
thinly traded ones — tend to have wider spreads. Pre-market and
after-market hours for US stocks are also thinner than regular hours,
with spreads that tend to widen.

In other words, a CFD rate is built in the order "index → futures →
CFD rate," two steps removed from the index (for the processing from
futures to CFD rate, see item ① under "Where I would have stumbled
three years ago" in ["How Are Rates
Generated?"](./cfd-pricing-and-cover.en.md)). As the first subsection
showed, whether the reference is futures changes both whether there's
a rollover and which adjustments apply. Checking "what does this CFD
reference?" first is the starting point for understanding differences
by product type.
(Note that some brokers offer index CFDs that reference the index
itself rather than futures, with no contract month.)

A few other easy misunderstandings, for reference:

- Assuming "Japan 225 has the same terms wherever you trade it": even
  under the same Japan 225 name, terms change depending on which
  exchange's futures — or the index itself — is referenced. CME's
  Nikkei 225 futures, for example, come in both yen and dollar
  versions, so the currency depends on the reference. And referencing
  futures means rollovers and price adjustment amounts, while
  referencing the index itself means no contract month and no
  rollover. Same name or not, you can't know the terms without
  checking the reference.
- Assuming "leverage is the same for every product": for retail CFDs
  in Japan, the leverage cap differs by product type (as of writing,
  10x for equity indices, 20x for commodities, 5x for single stocks
  and ETFs). It's easy to mix this up with FX's 25x, but with the same
  ¥100,000 of margin you can trade up to ¥1,000,000 on an equity index
  CFD but only ¥500,000 on a single-stock CFD. The caps aren't set by
  volatility alone, though: caps for equity indices, single stocks,
  and the like are set at a level roughly meant to cover one day's
  price movement, while commodity CFDs have their caps set separately
  under a different law (the Commodity Derivatives Act) (see
  ["Leverage and Margin"](./cfd-basics.en.md)).
- Assuming "if the rate hasn't changed, P&L is zero": holding a long
  on a product that stays in contango means paying the price
  adjustment amount at every rollover, so P&L gets whittled down even
  when the rate is back where it started (see the example under "What
  happens if you hold a long for one month?" and the note in the
  ["rollover"](./cfd-rollover-and-adjustments.en.md) section).
- Assuming "the VIX number in the news equals the VIX CFD rate": it's
  the same structure as Japan 225. VIX is a calculated number that
  can't be traded directly, so a VIX CFD references VIX futures. In
  normal times VIX futures tend to be in steep contango, so the
  futures price is often above the VIX number. Even when the news
  reports VIX at "15," it's perfectly normal for the CFD rate to be
  above 15. Even if a product is named after an index, if its
  reference is futures, it won't match the index number.

#### Summary

From indices and commodities to US stocks and ETFs, product types
differ in many ways — whether there's a rollover, which adjustments
apply, currency, trading hours, leverage caps, and even how
operations responds. But every one of those differences starts from
the same place: "what does this CFD reference (futures, a single
stock/ETF, or spot)?"

When you come across a new product, check its reference first. Once
you know the reference, this section's framework gives you a pretty
good idea of whether it rolls over, which adjustments apply, and
what to watch out for.
