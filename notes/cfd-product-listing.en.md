# CFD Notes: Adding a New CFD Product in Practice

🇯🇵 [日本語版](./cfd-product-listing.md)

[← Back to the CFD notes index](./cfd.en.md)

This file covers what gets considered and prepared when a broker starts
offering a new CFD product.

---

### Adding a New CFD Product in Practice (How a New Product Gets Launched)

The other files in these CFD notes explain how CFDs work (references,
rollover, adjustments, cover, and so on). Building on that, this
section lays out what gets considered and prepared when a broker
starts offering a new CFD product.

#### What does the overall flow of adding a product look like, in a nutshell?

Adding a product moves through four broad stages: "decide whether to
do it" → "decide how to sell it" → "prepare how it will run" →
"prepare how to announce it."

| Stage | Step | What gets decided or checked |
|---|---|---|
| 1. Decide whether to do it | Assessing the product's appeal | Is it attractive to clients, is there demand, is it marketable, and can enough trading volume be expected to make it worth offering? |
| | Checking cost-effectiveness | Does it justify costs such as data usage fees (data license fees)? If the product needs recurring work, can enough revenue be expected to justify that work? Check with data vendors whether the data can be licensed for this use and what it costs |
| 2. Decide how to sell it | Reference exchange and trading hours | Which exchange to reference, and from what time to what time trading will be offered |
| | Spread | Taking risk and revenue into account, how wide the spread (the gap between bid and ask) needs to be |
| | Trading rules | Whether any special trading rules are needed; setting trading limits (per order, per day, open position size) and the like |
| 3. Prepare how it will run | Data integration | Work with data vendors to start getting price data flowing into the broker's systems; coordination with engineers is also needed |
| | Market risk weighting | For each product, confirm which category it falls into for the regulatory market risk calculation (the weighting for each category is set by law), and decide the settings used for internal risk management (internal weightings, position limits, and so on) (see ["Position Limits and Cover Strategy"](./cfd-pricing-and-cover.en.md)). Since this is configured in the system, it's also confirmed with the finance team |
| | Pricing parameters and cover settings | Set the pricing parameters (how the spread is determined, the thresholds for flagging abnormal rates, and so on — covered in detail under "How are the trading rules decided?"). Also select the cover counterparty and set the position limit (the position size above which automatic cover trades are triggered) and the maximum size of each cover trade |
| 4. Prepare how to announce it | Preparing for launch | Writing the client-facing trading rules, compliance review (checking that advertising and explanations meet regulations), announcements, and preparing historical data for charts |

Note that the "prepare how it will run" stage requires preparation
with both the party that sends price data (the data vendor) and the
party that takes the cover trades (the cover counterparty). These are
basically separate parties, and contracts and connections need to be
set up with each (see "What gets checked on external costs and data
preparation?").

The order exists because what's decided in each step becomes the
premise for the next:

- "Whether to do it" comes first because, without product appeal and
  cost-effectiveness, everything after it would be wasted effort.
- Within "how to sell it," the reference exchange and trading hours
  come first. Which exchange and which hours are referenced changes
  the liquidity (how actively it trades), and that in turn is the
  input for setting the spread and trading limits. Reviewing trading
  hours can even change the decision about whether to add the product
  at all.
- "How it will run" can't be decided until the selling terms
  (exchange, hours, spread, trading rules) are set — otherwise it's
  unclear what to configure in the system.
- "How to announce it" comes last, once all the rules are settled.

#### How are candidate products narrowed down?

There's no absolute rule that cleanly says "meets this condition, so
it's OK; doesn't, so it's not" when deciding whether to offer a new
product. The rough benchmark is whether you can "tell a story that
makes a reasonable case for adding this product" — that is, whether
you can lay out, in a logical way and from the angle each stakeholder
cares about, why this product should be added.

**What gets checked**

| Angle | What's checked |
|---|---|
| Does it work as a business? | Is it attractive to clients, is there demand, is it marketable, can enough trading volume be expected, and can the broker secure the minimum revenue it needs? |
| Cost-effectiveness | Can revenue be expected to justify data usage fees (data license fees) and system development costs? If it needs recurring work, is that worth it? |
| Can it be covered? | Is there enough liquidity (trading activity) in the cover counterparty's market? Is it a market the current cover counterparties can route orders to (unless a new cover counterparty is being added)? |
| Can it be offered under laws and regulations? | See below |
| Can it be offered under contracts? | Do the terms of use of the exchange or data vendors restrict how the data can be used (e.g., redistribution to clients)? For an equity index, is a license needed from the index provider (Nikkei Inc. for the Nikkei 225)? |

Which exchange and which hours are referenced also changes the
expected liquidity and trading volume. Reviewing trading hours can
change the decision about whether to add the product at all, so when
that's a possibility, trading hours are considered together at this
stage.

**What to check from a legal and regulatory angle**

- Which products the broker is allowed to offer: the governing law
  differs by type of CFD. CFDs on equity indices and single stocks
  fall under the Financial Instruments and Exchange Act. Commodity
  CFDs such as oil and gold can't be offered without a license under
  the Commodity Derivatives Act. The first hurdle is whether the
  broker is qualified to offer that product at all.
- Industry self-regulation: the body that sets the rules differs by
  product. The Japan Securities Dealers Association covers CFDs on
  equity indices and single stocks, the Financial Futures Association
  of Japan covers currency-related products such as FX, and the
  Commodity Futures Association of Japan covers commodity CFDs such as
  oil and gold, each setting its own self-regulatory rules. In
  practice, though, which association's rules a broker follows
  depends on which associations it belongs to, and many brokers belong
  to more than one. The leverage that can be offered to retail clients
  is also capped by law for each product type. Laws and rules can
  change, so when adding a new product, the rules in force at that
  time need to be checked.
- How easily it can be explained to clients: when offering a product
  to retail clients, the question is whether its risks can be
  properly explained (the suitability principle — not soliciting in a
  way that is inappropriate in light of the client's knowledge,
  experience, financial situation, and investment objectives — and
  the duty to explain). Products with complex mechanics or unusual
  price behavior, like VIX CFDs or leveraged ETFs, need more thorough
  explanatory materials and warnings. Advertising content is reviewed
  as well.
- Products that need extra care: products linked to sanctioned
  countries or entities can't be offered. Some products, such as
  shares of the broker itself or its affiliates, also need care from
  a conflict-of-interest standpoint (where the broker's and clients'
  interests collide).

**Who is the story told to?**

The main audience is internal approvers, but the same story ends up
doubling as the explanation for several audiences.

| Audience | What they care about |
|---|---|
| Management / internal approvers | Does it work as a business (demand, trading volume, profitability, cost-effectiveness)? |
| Risk management / finance | Can the broker bear the market risk it takes on and the burden on its capital? Is there enough liquidity to cover? |
| Compliance | Can it be offered under laws and self-regulation? Can it be explained to clients? |
| External parties (cover counterparties, data vendors, index providers) | Do the contracts allow order routing, and use and redistribution of the data and the index? |

**The most common sticking point is cost-effectiveness**

Of all these angles, the one most likely to cause trouble in practice
is cost-effectiveness. Adding even a single product brings a range of
costs and work, while how much revenue it will bring can't really be
known until it's actually offered.

The costs and work involved include:

- Data costs: data usage fees paid to exchanges and data vendors.
  Adding a product can create new costs on top of what's already
  being paid. Costs also aren't always charged per product — they may
  be charged per exchange or as a package. Adding one more product
  from an exchange already in use costs little, but connecting to a
  new exchange for the first time costs a lot. So a single product may
  not pay for itself, while adding several products from the same
  exchange together does.
- System development costs: development is needed together with
  engineers, such as integrating price data into the broker's systems
  and configuring how rates are generated.
- Recurring work: some products generate periodic work — for example,
  rollovers for products referencing futures (setting price
  adjustment days), dividends on single stocks and ETFs (registering
  rights adjustments, i.e., adjustments for dividends and other
  shareholder rights; often called "dividend adjustments" in the
  industry), and handling stock splits and reverse splits. Leveraged
  and inverse ETFs in particular often carry out repeated reverse
  splits. A leveraged ETF is designed to track a multiple (such as 2x
  or 3x) of the underlying index's daily move, and an inverse ETF is
  designed to move in the opposite direction. Some combine the two,
  such as -3x (e.g., SOXS, which tracks -3x the daily move of a
  semiconductor index). Because these ETFs rebalance every day to keep
  their multiple, they tend to lose value in volatile markets, and
  they reverse-split so their price doesn't fall too low (e.g., SQQQ,
  which tracks -3x the Nasdaq-100, has done 1-for-5 reverse splits
  every few years). Each one needs handling.
- Explanation and review work: the more complex a product's
  mechanics, the more work goes into client-facing explanatory
  materials and advertising review.
- Competing for limited staff resources: engineering and operations
  staff are limited. Priorities have to be set against other
  projects, and the comparison "could that time make more money if
  spent elsewhere?" (opportunity cost) also comes up.
- The cost of stopping: once a product is offered, it can't easily
  be dropped. Ending it means giving clients a notice period and
  having remaining positions closed. That makes "just try it, and
  drop it if it doesn't work" a hard call, so the review before
  launch tends to be careful.

On the revenue side, meanwhile, there's uncertainty such as:

- Trading volume is hard to predict: how many clients will trade, and
  how much, isn't known until it starts.
- The spread can't necessarily be set wide: most revenue comes from
  the spread, but without spreads as tight as competitors', clients
  won't come. Tightening spreads to win volume cuts the revenue per
  trade.
- Cover costs: if liquidity in the reference or cover market is low,
  the cost of cover trades (such as slippage) grows and squeezes
  revenue.

In other words, the part of the story that's questioned most is
whether you can explain that the product is still worth adding after
weighing the costs and work that are certain up front against
revenue that isn't known until it starts.

#### How are the trading rules decided?

Trading rules define the terms on which clients trade. Many of them —
trading hours, tick size, contract size — end up on the client-facing
product list. The main items decided are:

| Item | What gets decided |
|---|---|
| Trading hours | Which exchange to reference, and from what time to what time trading is offered |
| Tick size | The minimum increment in which the distributed price (the quote) moves (e.g., ¥1 steps, $0.01 steps) |
| Contract size | Quantity per lot (e.g., ¥10 × the index, 10 barrels), minimum trade size (the smallest number of lots that can be traded), and lot increments (whole lots or 0.1-lot steps) |
| Trading limits | Maximum quantity per order (maximum order size), the daily trading limit, and the limit on open position size |
| Which adjustments apply | Which of the price adjustment, rights adjustment, and interest adjustment apply |
| How the price adjustment day is chosen | For products referencing futures, when to roll over |
| Spread | How wide the gap between the bid and ask shown to clients should be |
| Pricing parameters | The finer points of how the spread is set, and the thresholds that protect clients from abnormal rates |

**Trading hours**

After checking the reference exchange's trading hours and liquidity
by time of day (executed volume and quoted size by hour), the broker
sets its own trading hours. The thinking is:

- Don't extend beyond the reference exchange's hours (matching them
  exactly is fine). Accepting trades while the reference is closed
  would mean there's no underlying price and no way to cover.
- Avoid offering trading during hours when liquidity is extremely
  low.

This principle doesn't apply as is to every product, though. For a
product like Japan 225, which switches the referenced exchange by
time of day, the hours are based not on a single exchange's hours
but on the hours when a referenceable price exists, including the
exchange it switches to. For a product with no exchange, traded
bilaterally like spot gold, the benchmark is the hours when the cover
counterparty quotes prices and accepts trades.

The liquidity by time of day checked here also feeds into the spread
and trading limits decided next.

**Trading limits**

Limits are set per order, per day, and on open position size. For a
new product, the question is whether to place it into an existing
group (a group of products with similar characteristics) or create a
new group.

**Which adjustments apply, and how the price adjustment day is chosen**

Which adjustments apply is decided by the reference (see "Do rollover
and adjustments work differently by product type?" in ["Examples by
Product Type"](./cfd-product-types.en.md)). For products with rights
adjustments, whether dividends are subject to withholding tax is
confirmed with tax specialists in advance. For products referencing
futures, how the price adjustment day is chosen is also decided. The
benchmark is "the day when liquidity in the near and far months is
just about to flip," and it differs by product — just before SQ (the
Special Quotation, i.e., the final settlement price) for equity
indices, before the last trading day for crude oil (how many business
days before varies by broker), well before the last trading day for
grains, and so on (see "Do rollover and adjustments work differently
by product type?" in ["Examples by Product
Type"](./cfd-product-types.en.md)).

**Spread**

The baseline for the spread is to match competitors' spreads. Fewer
brokers offer CFDs than FX, so there aren't many reference points for
deciding. Using cues such as the gap between the reference exchange's
best quotes (the best bid and best ask) and the spreads of
competitors that already offer the product, the spread is set by
balancing risk and revenue.

The spread also isn't necessarily the same all the time. It may be
varied by time of day — tighter when liquidity is high, wider when
it's low. It may also be changed around times when the market tends
to move sharply, such as before and after economic data releases.
When liquidity is low or the market moves suddenly, the reference
price itself tends to jump and cover trades tend to get more
expensive.

**Pricing parameters**

Beyond the overall level of the spread, the finer parameters used to
build the rate are set as well. The main ones are:

- How the spread is set: approaches include deciding how much to add
  on top of the reference price's spread when quoting to clients, or
  normally fixing the spread at a set value, widening it when the
  market gets rough and the spread exceeds a certain range, and then
  stepping it back to the fixed value once things calm down.
- A spread cap: setting a ceiling so the spread never widens beyond a
  certain level, however rough the market gets.
- Liquidity-based spreads: setting the spread to apply according to
  the liquidity (the quoted size) of the prices received from the
  data vendor.
- Abnormal rate detection thresholds: thresholds for halting rate
  distribution or rate generation. They're usually defined as a
  combination of how far the price has moved and how long that
  state has lasted. The actual values differ by broker and generally
  aren't disclosed (see "Halting distribution of abnormal rates"
  under "Where do I (in operations) monitor rate generation and
  distribution?" in ["How Are Rates
  Generated?"](./cfd-pricing-and-cover.en.md)). The main cases are:
  - At the open, the previous close and the day's opening price are
    far apart (a gap)
  - The price moves by more than a set amount from the previous tick
    (the last price received) (distribution is halted for a set time)
  - A move of more than a set amount continues for longer than a set
    time (rate generation itself is temporarily halted)
- Monitoring divergence between data vendors: thresholds for raising
  a warning or error when prices received from multiple data vendors
  drift apart by more than a set amount.

These parameters aren't set once and forgotten. Market conditions
(the size of price moves, liquidity) and competitors' spreads keep
changing, so the parameters are reviewed and adjusted to match. Since
the right values change with the market, this is one of the most
time-consuming and difficult parts of the trading rules.

#### What gets checked on external costs and data preparation?

Offering a new product requires preparing to receive its price data
and preparing to be able to cover it. Both involve working with
outside companies, and it takes time to go from checking costs and
contracts to actually getting things working (going live).

**Checking filings and reports**

Depending on the type of product, adding it may require filings or
reports to the supervisory authorities or self-regulatory bodies.
Commodity CFDs, for example, require a license under the Commodity
Derivatives Act in the first place, and even for a broker that
already offers them, depending on what's being added, a change
notification to the competent ministries (MAFF and METI) or a report
to the Commodity Futures Association of Japan may be needed. The
required procedures vary with what's being added, and laws and rules
can change, so this is checked with the compliance team in advance.

**Checking data costs**

First, the data fee structure is checked with the exchange and the
data vendor. The key point is "will adding this product increase
costs?" For single stocks, corporate information data is checked in
addition to price data. If a new cost arises, internal approval (a
formal sign-off process) is needed. Separate from fees paid annually,
pro-rated charges for just the added product may be billed mid-term,
so it's important to know which costs arise when.

**Work with data vendors, and going live**

The work required differs by data vendor. The main tasks are:

- Signing a market data agreement
- Paying exchange and vendor data fees
- Submitting usage declarations to the exchange (e.g., how the data
  will be used)
- Subscribing to the added product on a data terminal

Depending on the vendor and the product category, the existing
contract may already cover it and no extra work is needed. Once the
procedures are done, price data is made to arrive correctly in the
broker's systems (going live).

**Contracts with cover counterparties, and going live**

Without cover trades, the risk taken on from client trades can't be
passed on. So contracts and connections are set up so the new product
can be traded with the cover counterparty. Especially for products
covered through bilateral trading with banks and the like, such as FX
and spot precious metals, the trading agreement with the cover
counterparty may need to be amended or supplemented. Bilateral
derivatives trading typically uses agreements such as an ISDA Master
Agreement (the industry-standard master agreement on the form of the
International Swaps and Derivatives Association) and a CSA (Credit
Support Annex, governing the exchange of collateral), and the terms of
these agreements may be revisited when handling a new product. For
products covered with exchange-traded futures, on the other hand, what
is needed is an account agreement with the clearing broker that
executes and clears the futures orders, a connection to the exchange,
and an agreement for using its market data. If execution and clearing
are split between different firms, a give-up agreement setting out
that arrangement is also signed. With futures, the exchange's
clearing house takes on the counterparty risk, so agreements like an
ISDA Master Agreement or a CSA, which set collateral terms one-to-one
with the counterparty, aren't needed. Once the contracts are in place,
things are set up so cover orders can actually be sent and executions
come back (going live).

**Why this needs special care**

Of all this, the work with data vendors and going live, and the
contracts with cover counterparties and going live, take the most
effort and directly affect clients and revenue, so they get special
attention.

- If something goes wrong with the data going live, correct prices
  won't arrive, and wrong rates may be sent to clients.
- If something goes wrong with the cover counterparty going live, the
  risk from client trades can't be passed on, and the broker is left
  carrying market risk.
- Both involve outside companies, so the broker can't move ahead on
  its own. If preparation slips, the launch date itself slips, and the
  expected revenue is pushed back too.

**Historical data for charts**

Historical price data is prepared for the charts clients see on the
trading screen. Several years of daily bars with open, high, low, and
close (OHLC) are prepared, and weekly and monthly bars are built from
them. For products referencing futures, how to join the historical
data where the contract month switches is also decided. Approaches
include joining the contracts as is without adjustment (a gap remains
on the rollover day), adding or subtracting the price difference
between the near and far months to the earlier data (price ranges
are preserved, but past prices no longer match the actual ones and
can even turn negative), and multiplying the earlier data by the
price ratio (percentage changes are preserved, but price ranges no
longer match the actual ones); which one is used differs by broker.
Shorter bars such as 1-minute and 30-minute bars are built from
real-time rates, so this is coordinated with the systems side early.
The prepared data is double-checked. The main checks are the date
definition for daily bars (what time of day a day is cut off), the
formulas, and whether the OHLC for randomly chosen weeks and months
match.

#### How does the setup work change by product type?

The setup work when adding a product varies a lot with the reference.
Here, the work needed when adding a product is organized by reference
(for how day-to-day operations differ by product type after launch,
see "Do I (in operations) handle things differently depending on
product type?" in ["Examples by Product
Type"](./cfd-product-types.en.md)).

**Products referencing futures (indices, commodities)**

- Set the principle for the price adjustment day and add the product
  to price adjustment (rollover) operations: the benchmark is "the day
  when liquidity in the near and far months is just about to flip,"
  and it differs by product — just before SQ for equity indices,
  before the last trading day for crude oil (how many business days
  before varies by broker), well before the last trading day for
  grains such as corn and soybeans (see "Do rollover and adjustments
  work differently by product type?" in ["Examples by Product
  Type"](./cfd-product-types.en.md)).
- Register contract-month information: register the information on
  which contract month is referenced from when to when (the
  contract-month master data) for the new product too.
- Check how the referenced futures settle: check whether they're
  cash-settled at expiry (like Nikkei 225 futures) or involve physical
  delivery (like WTI crude futures). For products with delivery, the
  cover position has to be rolled before delivery, so that deadline is
  decided from the start. This deadline is set on a different basis
  from the client-facing price adjustment day (which follows where
  liquidity moves). For example, WTI crude futures have to be rolled
  by the last trading day, while grain futures such as corn and
  soybeans have to be rolled before the First Notice Day (the first
  day on which delivery notices can reach holders of long positions),
  which falls before the delivery month.
- Set up contract size conversion: for cover trades, set how many CFD
  lots equal one futures contract.
- Set up switching of the referenced exchange: for products that
  switch the referenced exchange by time of day, like Japan 225, set
  which exchange is referenced in which hours.

**Products referencing single stocks or ETFs**

- Prepare the first rights adjustment: for the first rights
  adjustment after launch, check the dividend announcement in advance
  on a data terminal or similar, and register it once it can be
  registered in the system. If the launch coincides with an ex-date,
  confirm in advance so the registration is in time (for the rights
  adjustment itself, see ["When a Dividend Is Paid (Rights
  Adjustment)"](./cfd-rollover-and-adjustments.en.md)).
- Check withholding tax: whether dividends are subject to withholding
  tax, and at what rate, depends on the tax rules of the country where
  the issuer (the company, or the fund for an ETF) is resident, so this
  is confirmed with tax specialists in advance.
- Register interest adjustment day counts: register in the system the
  day counts used to calculate interest adjustments (the days counted
  together when a position is held over a weekend or holiday).
- Add it to corporate action monitoring: add the new product to
  monitoring so splits, reverse splits, spin-offs, and the like aren't
  missed (see ["When a Spin-off, Reverse Split, or Stock Split
  Happens"](./cfd-rollover-and-adjustments.en.md)).
- Check how shorts are handled: check securities lending (stock
  borrowing) conditions and short-selling restrictions, and decide
  whether to accept shorts from the start.
- Know upcoming events such as earnings: keep track of scheduled
  events likely to move the price sharply, such as earnings release
  dates.
- Check ETF-specific points: check distribution frequency (monthly,
  quarterly, etc.), how often it splits or reverse-splits (leveraged
  and inverse ETFs reverse-split often), whether it's an ETF that
  holds futures, and whether it's leveraged (for ETF characteristics,
  see "Index, commodity, and US stock/ETF CFDs — what's the
  difference, in a nutshell?" in ["Examples by Product
  Type"](./cfd-product-types.en.md)).

**Products referencing spot (spot gold, etc.)**

- Set up the interest adjustment: decide where the interest rate used
  to calculate the interest adjustment comes from and how it's set.
- Register interest adjustment day counts: in line with how the value
  date is counted, register the days counted together when a position
  is held over a weekend or holiday (for spot products, as with FX,
  the Wednesday rollover often counts three days; this varies by
  broker).
- Check contracts with cover counterparties: for products covered
  through bilateral trading with banks and the like, the trading
  agreement with the cover counterparty may need to be amended or
  supplemented (see "What gets checked on external costs and data
  preparation?").

**Things that change with the reference market (common to all product types)**

- Register market holidays: register the reference market's holidays.
  For a country's market handled for the first time, a new calendar
  for that country is prepared.
- Handle daylight saving time: for markets with daylight saving time,
  set when it switches and the resulting changes to trading hours.
- Handle a new currency: for a product in a currency handled for the
  first time (e.g., the first Hong Kong dollar product), a new exchange
  rate for converting into yen (the FX conversion rate) is prepared.
- Decide the market risk category: decide which category the product
  goes into for the regulatory market risk calculation (equities,
  including equity indices; gold; commodities other than gold; and so
  on), and set the corresponding weighting in the system. For an
  equity index, whether it counts as a "major equity index" under the
  rules also changes the calculation. For products denominated in a
  foreign currency, FX risk is calculated separately as well. The
  weightings and limits used for internal risk management are decided
  at the same time (see "What does the overall flow of adding a
  product look like, in a nutshell?").
- Check filings and reports: depending on the type of product, filings
  or reports to the supervisory authorities or self-regulatory bodies
  may be needed (see "What gets checked on external costs and data
  preparation?").

Any of these, if missed, directly affects client accounts or the
broker's risk, so they all call for care regardless of product type.

#### Where do I (in operations) fit into adding a product?

Which department handles adding a product differs by company. It's
often an operations team member who serves as the lead, in which case
they're involved in all four stages laid out under "What does the
overall flow of adding a product look like, in a nutshell?"

**The lead's role: connecting the departments involved and getting to launch**

The lead's role is to take all the considerations and preparation
described so far, sort and confirm them one by one with the
departments involved, and get the product to launch within a few
months. Rather than deciding everything alone, it's closer to
gathering what each department is responsible for and pulling the
whole picture together so nothing falls through the cracks or
conflicts.

| Who to work with | Main things to confirm |
|---|---|
| Marketing | Is the product attractive to clients, is it marketable? Preparing announcements and product pages |
| Corporate planning | Preparing the press release |
| Engineers (systems) | Data integration, settings for generating rates, preparing chart data |
| Risk management / finance | Market risk weighting, trading limits and position limits |
| Compliance | Whether it can be offered under laws and self-regulation, whether filings or reports are needed, review of trading rules and advertising |
| Tax specialists | Whether withholding tax applies when there are rights adjustments |
| Client support (call center) | Sharing the trading rules and points of caution so they can answer questions about the new product |
| Data vendors | Data costs, contracts, subscription procedures, going live |
| Cover counterparties | Trading agreements, whether orders can be routed, going live |

**How the client-facing trading rules and product pages are made**

The client-facing trading rules and product pages directly involve
business requirements (trading hours, contract size, trading limits,
etc.), so the lead's side takes the main role in writing them. The
process generally goes in this order:

1. Write the draft
2. Coordinate the content and how it's displayed with marketing and
   systems
3. Request advertising review (compliance checking that the wording
   meets regulations)
4. Request creation of the pages and other content

Only after passing compliance's advertising review can it be
published to clients.

**What gets checked before and after launch**

Checks happen in two stages: before and after launch.

First, before launch, user acceptance testing (UAT: testing from the
standpoint of those who use the system, to confirm it works as the
business requirements specify) is carried out in a staging
environment (a test environment set up with the same configuration
as production), covering as many expected events as possible. In
addition to rate generation and distribution, client trading, cover
trades, and reconciliation, events that wouldn't happen in production
until some time has passed — such as price adjustments (rollover)
and rights adjustments — are deliberately triggered in the test
environment to confirm they work.

Then, after release to production, checks continue in stages. All of
the items below are assumed to have already been checked once in the
test environment before launch. The checks after launch are there to
re-confirm that things work as tested in the real production
environment, with real market data and real client trades.

1. Right after launch
   - Are rates being generated and distributed correctly?
   - Can clients trade?
   - Are market, limit, and stop orders each accepted and executed
     correctly?
   - Are charts, the product list, and other client screens displayed
     correctly?
   - Does what's written in the client-facing trading rules and
     announcements (trading hours, contract size, trading limits,
     etc.) match the actual system settings?
   - Are trading limits and spread settings working as intended?
   - Are the abnormal rate detection thresholds neither too strict
     (halting distribution more than necessary) nor too loose (missing
     abnormal rates)?
   - Is the new product included in monitoring screens and alerts,
     such as abnormal-rate monitoring and position monitoring?
2. Once trading has started
   - Are any problems showing up in reconciliation (matching the books
     against actual balances and positions)?
   - Are cover trades working normally? When the position limit is
     exceeded, do automatic cover trades trigger as intended?
   - For products that switch the referenced exchange by time of day,
     is the switch happening correctly?
   - Is the required margin rate set correctly and reflected in the
     margin level calculation?
   - Do stop-outs (forced liquidation) work correctly?
   - For products in currencies other than yen, such as USD, is P&L
     converted into yen at the correct exchange rate (FX conversion
     rate)?
   - Do the start and end of trading hours, and the processing that
     spans the day boundary, work correctly?
   - Do daily processes such as daily mark-to-market (end-of-day
     processing) and applying interest adjustments work correctly?
   - Are positions in the new product correctly reflected in the
     market risk calculation?
   - Does the new product appear correctly in client trade
     confirmations and statements, and in reports to regulators and
     others?
   - Trading volume and client inquiries over the first few days
3. At the first events
   - At the first price adjustment and the first rights adjustment,
     are payments to and from clients made correctly (including the
     conversion into yen for products in other currencies)?
   - At the first market holiday and the first daylight saving time
     switch, do trading hours and the like switch correctly?

   Even if confirmed in the test environment, whether things work with
   real market data and real client positions is re-confirmed when
   each event actually arrives.

#### Where I would have stumbled three years ago

Assuming "adding a product = just registering one more product in the
system"

From a client's point of view, a new product looks like one more row
suddenly appearing in the product list on the trading screen one day.
So adding a product can seem like a task that's done once the product
is registered in the system.

In reality, adding a product is a project that takes several months.
Behind that one row are the four stages laid out under "What does the
overall flow of adding a product look like, in a nutshell?":

- "Whether to do it": is it attractive to clients, is it worth the
  cost, can it be offered under the law?
- "How to sell it": trading rules such as trading hours, spread, and
  trading limits
- "How it will run": contracts with and going live with data vendors
  and cover counterparties, market risk weighting, pricing parameters
- "How to announce it": writing the trading rules, compliance review,
  announcements

These are worked through one by one with many parties — marketing,
engineers, risk management, compliance, outside companies, and more.
That one row in the product list can only appear once all of that
preparation is in place.

A few other easy misunderstandings, for reference:

- Assuming "a good product should be added": even a product that's
  attractive to clients isn't added on that basis alone. The biggest
  hurdle in practice tends to be cost-effectiveness — especially
  whether revenue can be expected to justify system development costs
  and recurring work such as rollovers, dividends, and splits and
  reverse splits (see "How are candidate products narrowed down?").
- Assuming "as long as the data comes in, prices can be quoted":
  quoting prices and being able to cover are separate matters. The
  data vendor that sends price data and the cover counterparty that
  takes cover trades are basically separate parties, and the product
  can't be offered unless contracts and going live are in place with
  both. If prices can be quoted but cover isn't possible, the risk
  from client trades can't be passed on and the broker is left
  carrying market risk (see "What gets checked on external costs and
  data preparation?").
- Assuming "once it's launched, the job is done": after launch,
  checks continue each time a first event arrives — the first price
  adjustment and rights adjustment, the first market holiday, the
  first daylight saving time switch (see "Where do I (in operations)
  fit into adding a product?"). The pricing parameters also keep being
  reviewed afterward in line with market conditions and competitors'
  spreads (see "How are the trading rules decided?").
