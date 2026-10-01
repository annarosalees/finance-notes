# CFD Notes: Pricing and Risk Management (Rate Generation, Cover, Position Limits)

🇯🇵 [日本語版](./cfd-pricing-and-cover.md)

[← Back to the CFD notes index](./cfd.en.md)

This file covers how the rates quoted to clients are built, and how the
risk taken on from client trades is handled and managed (cover deals
and position limits).

---

### How Are Rates Generated?
A CFD's rate is generated independently by the broker, based on the
exchange price of whatever it references (a futures contract or the
physical asset). The broker doesn't simply pass that reference price
straight through to clients, though.

A CFD's rate also isn't a single number — it's quoted as two values,
an ask (buy) and a bid (sell). The gap between those two values is
the spread, which is the CFD's real underlying cost.

The reason it's quoted as two values instead of one is that a CFD is
an over-the-counter (OTC) product, not an exchange-traded one. There's
no order book publicly showing supply and demand the way there is on
an exchange, so the broker itself quotes a bid and an ask and takes
the difference — the spread — as its effective fee.

#### How the referenced futures/physical price relates to the rate
A CFD's rate moves in step with the exchange price of whatever it
references (futures or physical). For products that roll over,
though, "which contract month is currently being referenced" has a
direct effect on the rate, which makes managing the reference month
especially important.

#### A concrete example: where do the rates for Japan 225 or WTI crude oil actually come from?
Raw exchange data is difficult to work with as-is, so it's usually
supplied in a cleaned-up form — as tick data or one-minute bars — by
major data vendors. A broker offering
CFDs receives real-time data from one of these providers, layers on
adjustments like the spread, and generates the rate it quotes to
clients.

It's technically possible to source data directly from an exchange,
but that means setting up a connection and a contract with every
individual exchange, which adds development cost. If a broker offers
20 different products, for example, contracting with a data provider
is far more efficient — both contractually and in terms of system
development — than connecting individually to every exchange
involved (CME, ICE, NYSE, and so on).

Brokers also typically contract with more than one data provider, so
that an outage at one provider doesn't have to interrupt the rates
quoted to clients (more on this below).

#### Where does operations (me) monitor rate generation and distribution?
Operations continuously monitors two things: that rates never stop
flowing, and that they never drift away from where the market
actually is.

- Deciding on failover: if the main data provider has an outage and
  client-facing rates become abnormal (or stop being generated at
  all), the priority is the client — operations switches over to the
  secondary data provider. Before switching, operations checks the
  secondary provider's rate against actual market levels (using yet
  another provider not used for rate generation) to confirm there's
  no significant discrepancy. Investigating the root cause of the
  outage comes later; responding to clients comes first.
- Managing spread width: how wide the spread is set depends on the
  risk and cost profile of each product, and it's the broker that
  sets it.
- Monitoring for abnormal rates ("abort"): this doesn't refer to a
  sudden spike or drop in the market price itself — it refers to a
  mechanism that automatically halts processing before an incorrect
  rate reaches clients or the cover counterparty, when abnormal price
  movement is detected. That movement might reflect a genuine market
  event (a major economic data release, for example) or a data
  problem — the two can't be told apart in the moment. So the
  procedure is to pause distribution, confirm where the market
  actually is, and resume once there's no issue.

  Typical triggers for an abort include:
  - Stale pricing from latency: network delay causes a gap between
    the rate and the firm's own latest internal rate that exceeds a
    pre-set tolerance
  - Sharp volatility: around major economic data releases, for
    example, the market price moves so fast that price reliability
    temporarily can't be guaranteed
  - Detecting an outlier (a spike): the feed itself contains a bug or
    an abnormal value, and the system catches it

  Note that the rate generated for clients and the rate sent to the
  cover counterparty (a CP) are two different things, so a
  rejection on the cover side (so-called "last look") is, strictly
  speaking, a separate issue from rate generation. That said, using a
  cover side that's currently erroring out as a reference input for
  rate generation would be dangerous, so it's still something
  operations keeps in mind when monitoring rate generation (covered
  in more detail under "The idea behind cover deals").

  This term "abort" is internal shorthand — elsewhere in the
  industry it may be called "abnormal rate detection" or "price
  rejection."

- Post-trade monitoring: how often aborts happen, and which triggers
  are most common, is an important thing middle/back office keeps an
  eye on. A sudden spike in the abort rate, or an unnatural
  clustering of them, can be a sign of a system bug or a
  misconfiguration — so this monitoring includes reviewing order
  history and logs to confirm no client was unfairly disadvantaged.

#### Where my three-years-ago self would get stuck
Two points in particular are easy to mix up, so they're worth
spelling out a bit more.

**① Assuming "the rate is the exchange price itself"**

Looking at the rate on a CFD screen, it can look as if the exchange
price is simply flowing straight through. In reality, it goes
through three stages before it ever reaches the client: exchange
price → cleaned up by a data provider → generated into a final price
by the broker, spread and all.

In other words, a CFD's rate isn't "a copy of the exchange price" —
it's "a separate price the broker builds on top of the exchange
price." Not matching the reference price exactly isn't an anomaly;
it's simply how the mechanism works.

**② Treating "rate generation" and "cover (hedging)" as the same thing**

Everything described above under "rate generation" is purely about
what price gets shown to the client. Separately, "cover" — the
broker hedging its own risk externally — is about how the client's
order gets routed to a cover counterparty (a CP). These are two
different pieces of work, two different processes.

They can look connected, but they're not the same thing. For
example, rates can be generated and distributed to clients
completely normally while, separately, an order to the cover
counterparty gets rejected (last look). "Rates are being generated
correctly" doesn't necessarily mean "cover is also going through
correctly" — a distinction that's easy to conflate at first. This
gets covered in more depth under "The idea behind cover deals."

### The Idea Behind Cover Deals
A cover deal means holding a position outside the firm (with a cover
counterparty / CP) in the opposite direction to the client's order.

In the course of offering CFDs and similar products to clients, the
broker ends up holding the opposite side of the client's order for
itself. For example, if a client goes long (buys), the broker ends
up holding the opposite, a short (sell) position. That's a state of
carrying "market risk" — the risk of a loss from the price of a held
position moving.

If the broker let this market risk build up unchecked, a large market
move could seriously damage its own financial position. So it offloads
the position it's holding to an outside cover counterparty (CP) to
manage the risk down. This whole sequence of trades is called a
"cover trade," or a "cover deal."

A CFD is a bilateral (aitai, 相対) contract between the broker and the
client — a one-to-one agreement with no exchange in between. This
bilateral nature is what produces the following three-layer structure.

Example: a client opens a long "buy" position in a Nikkei 225 CFD

1. Client position: long ("buy") on the underlying (Nikkei 225)
2. Broker's client-facing position (the CFD itself): because it's a
   bilateral trade, the broker automatically ends up holding the
   opposite side — a short ("sell") — as the client's counterparty
3. Broker's hedge position (the cover): to offset the price-move risk
   from the short it's now holding, the broker holds a "buy" in the
   underlying or futures with an outside cover counterparty (CP)

The end result is that the position the broker holds externally for
hedging (a buy) points in the same direction as the client's original
position (also a buy). By running "short against the client" and
"long in the market" side by side, the broker mechanically creates a
state where its own P&L is offset no matter which way the market
moves (delta neutral).

The risk of loss from a held position's value moving as the price of
the underlying moves is called "delta risk." Delta is a sensitivity
measure: how much the value of your position moves when the price of
the underlying moves by 1 unit.

- A long position in the physical asset or futures: delta is +1. If
  the underlying rises 100 yen, the position's value rises by 100
  yen too; if it falls, the value falls.
- A short position in the physical asset or futures: delta is -1. If
  the underlying falls 100 yen, the position's value rises by 100 yen
  (i.e., a rise in price means a loss).

Being "exposed to delta risk" means your total delta across your
positions is tilted positive or negative — you're in a state where
"a move in one particular direction in the market will cost you"
(i.e., you're carrying directional risk).

An example of the delta risk a broker takes on: a client opens a
one-unit long ("buy," +1) position in a Nikkei 225 CFD. The broker,
as the counterparty, automatically ends up holding a one-unit short
("sell," -1) in Nikkei 225. The broker is now carrying "a delta of
-1." If the Nikkei then spikes upward, the loss on the broker's short
position grows without limit. This is the state of "delta risk being
left open (unhedged)."

A financial institution's business model is to earn steadily from
fees and spreads collected from clients, not to gamble on which way
the market will move. So it does the work of eliminating the delta
risk it's picked up — delta hedging. To offset its own "-1" delta,
the broker buys one unit of the Nikkei 225 (the physical index or a
future) with an outside cover counterparty (CP). The buy position at
the cover counterparty produces a "+1" delta, so the short against the
client (-1) plus the buy at the cover counterparty (+1) nets out to a
total delta of 0.

A state where the total delta across all held positions nets out to
zero is called "delta neutral."

Note that, for simplicity, this example treats "one CFD unit" and
"one unit at the cover counterparty" as the same size. In reality,
the two trade units often don't match. WTI crude oil futures, for
example, trade on the exchange at 1,000 barrels per contract, while
a broker may set a much smaller trade unit for the CFD. In that
case, cover trades require converting "how many CFD units equal one
futures contract" before deciding the quantity to trade with the
cover counterparty.

#### A concrete example: when a client opens a long position, what does the firm do?
Say a client opens a new long ("buy") order in a WTI crude oil CFD.
Because a CFD is a bilateral trade between the broker and the client,
the moment the client goes long, the broker automatically ends up
holding the opposite side — a short ("sell") position.

Left as is, the broker is now stuck holding a short position that
loses money if the oil price rises. So the broker places a matching
buy order with a cover counterparty (CP), taking a long position
there. This lets the broker offset (hedge) the risk from the short it
picked up with the client, using the opposite trade at the cover
counterparty.

In other words, the position created by the client trade and the
position created by the cover-counterparty trade point in opposite
directions (client long → broker short against the client → broker
long against the cover counterparty). This whole flow is what a cover
deal actually looks like in practice.

#### Where does operations (me) fit into confirming and executing cover trades?
The work operations does around cover trades breaks down into six
main areas.

**Checking trading-liquidity risk**

Operations regularly checks for "trading-liquidity risk" — the risk
that a cover trade can't be executed smoothly. Concretely, this means
checking the credit rating of cover counterparties (making sure
there's no credit concern), plus logging and analyzing any incident
where a cover trade wasn't executed promptly. The main causes fall
into four patterns:

- A system failure (at the firm itself, the cover counterparty, or
  the exchange) causing the cover to be rejected
- The cover being rejected because the exchange hit limit-down or a
  daily price-move limit
- The cover being rejected because the cover counterparty is short on
  margin, has hit a position limit, or triggers a margin call
- A carry-over caused by a corporate action (a stock split, merger,
  spin-off, etc.)

**Credit management of the cover counterparty (CP)**

The creditworthiness of the cover counterparty itself is also managed
on an ongoing basis. Metrics watched include: ratings from credit
agencies; CDS (Credit Default Swap — insurance-like protection that
pays out if the counterparty defaults; the higher the "premium rate,"
the stronger the signal of credit concern); whether exposure is overly
concentrated in one particular cover counterparty; and whether the
counterparty is a G-SIFI (Global Systemically Important Financial
Institution — a large international institution whose failure could
seriously disrupt the global financial system, and which is therefore
subject to special supervision).

**Timing and automating cover trades**

When covering manually, it's more efficient to do it during a
liquid period — when that instrument is most actively traded. Covering
during a thin-liquidity window tends to have a bigger price impact and
higher cost.

When covering automatically, a "cover limit" (the maximum tolerable
position size) is set in advance, and once that's exceeded, a cover
trade fires automatically. How that limit is set is worked out in
detail per broker and per instrument, and it ties directly into a
management-level judgment call: how much risk (position) the firm is
willing to carry (the relationship between limit size and
profitability is covered under "Position Limits and Cover Strategy").

**Day-to-day confirmation work**

This is an ongoing process: confirming execution details, reconciling
(matching the books against actual balances), checking the firm's own
positions, and confirming that the cover counterparty's margin
maintenance ratio and trading limits haven't been breached.

**Cover rollovers**

For products with a contract month (i.e., not perpetual), it's not
just the CFD itself that needs to roll — the cover counterparty
position also needs to roll from the near month to the next month.
The reference at the cover counterparty needs to be switched over too.

**How halt decisions are made**

When something goes wrong with cover trading or rate distribution,
the response is judged case by case, falling into three patterns:

- Cases where both cover and price should be halted: a delay in the
  rate feed from a cover counterparty, a cover counterparty's system
  failure meaning no rate or a bad rate, an inability to connect to
  a cover counterparty due to a problem on the firm's own side, etc.
- Cases where only cover should be halted: a large volume of
  unmatched trades with a particular cover counterparty, the cover
  counterparty approaching a position limit, etc.
- Cases where only pricing should be halted: cases where only some
  cover counterparties have unstable rates and other counterparties
  can still be used instead

#### Where my three-years-ago self would get stuck
The first time you hear about cover trades, the point of "why bother
doing an offsetting trade at all" can be hard to grasp. The key is
that the broker ends up carrying market risk it never wanted, the
instant it trades with a client. If a client goes long, the firm ends
up short, and that position's value moves with the price. A cover
trade is the act of pushing that "unwanted risk" out to an external
cover counterparty, bringing the firm's own position close to zero.
The thing worth internalizing early is that this is "a trade to avoid
holding risk," not "a trade to make money."

A few more misconceptions worth flagging:

- Treating "cover isn't working" as one single kind of problem: in
  reality there are three different kinds of causes — system/
  connectivity issues (a failure at the firm, the cover counterparty,
  or the exchange), issues in the market itself (price-move limits,
  liquidity drying up), and issues on the cover counterparty's side
  (a margin shortfall, hitting a position limit). Rather than lumping
  it all together as "the cover failed," in practice it matters to
  separate out which kind it is.
- Assuming "a client's loss = the firm's profit": as long as cover
  trades are being done properly, the risk created by a client's
  trade has already been pushed out externally, so a client winning
  or losing doesn't directly translate into the firm's own P&L.
- Assuming "the cover counterparty = the exchange": a cover
  counterparty is simply a financial institution the firm has a
  trading relationship with (a CP) — it isn't directly connected to
  the exchange the CFD references.
- Assuming "every single order gets covered individually": in
  practice, positions are often held in aggregate within the limit
  and covered once certain conditions are met, rather than being
  covered order by order. One likely reason is the difference in
  trade units: futures at the cover counterparty can't be traded in
  fractions of a contract, so it's hard to convert each small CFD
  order into futures one by one — the position is often covered once
  enough has built up to equal one futures contract.
- Conflating "a rejection from the cover counterparty" with "an abort
  on our own side": a rejection from the cover counterparty (so-
  called "last look") is the cover counterparty itself declining the
  trade it was offered. An abort, on the other hand, is the firm's
  own mechanism for temporarily halting the rate it distributes to
  clients and cover counterparties when it detects an abnormal
  value. These happen in different places, for different reasons —
  they're separate issues.

---

### Position Limits and Cover Strategy (Capital Adequacy and Market Risk Management)
The capital adequacy ratio is a metric showing how much financial
cushion a financial instruments business operator (a broker or an
FX/CFD firm) has to absorb an unexpected loss or a price swing on its
own. It expresses, as a ratio, how much readily usable capital the
firm has relative to the risk it's carrying.

$$\text{Capital Adequacy Ratio} = \frac{\text{Non-fixed capital}}{\text{Risk-equivalent amount}} \times 100$$

- Non-fixed capital (the numerator): capital minus fixed assets and
  the like — the portion that's readily convertible to cash or
  available to absorb risk
- Risk-equivalent amount (the denominator): the total of the risks
  the business can incur, converted into a monetary figure, made up
  of three components:
  - Market risk: the risk of loss from price moves in held positions
    (equities, commodities, etc.) — FX is covered separately, in
    `notes/fx.en.md`
  - Counterparty risk: the risk of loss from a trading counterparty
    (a cover counterparty or a client) defaulting or going insolvent
  - Operational risk: the risk of loss from system failures,
    processing errors, legal trouble, and the like

Under Japan's Financial Instruments and Exchange Act, a financial
instruments business operator is legally required to maintain a
capital adequacy ratio of at least 120% at all times (Article 46-6,
Paragraph 2). Regulatory measures escalate in stages: dropping below
140% triggers a mandatory filing with the FSA (Financial Services
Agency); dropping below 120% lets the FSA order changes to business
practices or require a deposit of assets, among other supervisory
measures; and dropping below 100% can lead to an order suspending all
or part of the business for up to three months. In practice, brokers
and FX/CFD firms typically manage themselves to a much higher safety
margin — 140–200% or more, day to day — using tools like position
limits and cover-deal operations, to stay ready for sudden market
moves or a spike in client positions.

#### How is market risk calculated?
Market risk is the risk of loss from a revaluation of a held
position. Under the law, when a financial instruments business
operator holds a position, a set proportion of it is calculated as
"market risk," which feeds into the risk-equivalent amount (the
denominator of the capital adequacy ratio). The calculation method
differs between equities and commodities.

**For equities**

- Market risk equals "net amount × 8% (general risk)" plus "gross
  amount × 8% (specific risk)."
- Net amounts can be netted within the same country (e.g., a long in
  the Dow and a short in the S&P 500 can be netted; a long in Nikkei
  225 and a short in the Dow cannot).
- Gross amounts are exempt for "major stock indices of designated
  countries" (Nikkei 225, S&P 500, DAX, FTSE, and so on). Also,
  unlike commodities, this isn't "gross across CP and client
  positions" — it only covers the uncovered (uncleared) portion.
- For foreign-currency-denominated names, an FX risk charge (held
  position × 8%) is booked separately on top of the above.

Concrete example: say a firm holds only a long position worth 10
million yen in a Nikkei 225 CFD. The net amount is 10 million yen, so
the net-side market risk is 10 million × 8% = 800,000 yen. Since
Nikkei 225 qualifies as a "major stock index of a designated
country," the gross-side 8% that would normally also apply is
exempted. So the market risk here comes out to 800,000 yen.

**For commodities**

- Gold: market risk equals "net amount × 8%." Under the law it's
  classified as an FX risk (gold's market risk = the absolute value
  of gold's uncovered position in yen × 8%).
- Everything else: market risk equals "net amount × 15%" plus "the
  sum of each instrument's gross position in yen × 3%." This gross
  position means "all positions across both CP and client sides,"
  and it's the sum of the absolute value of each position,
  regardless of buy/sell direction.
- Net amounts can't be netted across different instruments (e.g., a
  long in crude oil and a short in corn can't offset). Total
  commodity risk = SUM(absolute value of each held position × 15%).
- For foreign-currency-denominated names, an FX risk charge (held
  position × 8%) is booked separately on top of the above.

Concrete example: say a firm holds only a long position worth 5
million yen in WTI crude oil CFDs (a non-gold commodity). The net
amount is 5 million yen and the gross position is also 5 million
yen. The net-side market risk is 5,000,000 × 15% = 750,000 yen, and
the gross-side market risk is 5,000,000 × 3% = 150,000 yen, for a
combined market risk of 900,000 yen.

Note: the market risk calculation for FX is covered separately, in
`notes/fx.en.md`.

#### What is a position limit, and why set one?
A position limit is a cap on the size of the position (long or
short) a firm is allowed to hold. Along with some related terms,
it breaks down as follows:

- **Limit**: once the position size (long or short) exceeds this
  value, a cover trade is triggered.
- **Return level**: a cover trade is executed so that the resulting
  position size lands somewhere between this level and the limit.
- **Cover threshold**: a rough quantity (in units of the underlying)
  used as a guide when covering manually.

A position limit is set by working backward from an acceptable loss
tolerance. As covered above, the capital adequacy ratio is managed
day to day to stay within a 140–200%-plus safety margin. The firm
first decides how much loss it can absorb in a sudden market move —
in other words, how far the capital adequacy ratio can drop before
it breaches that safety margin — and then works backward from that
to arrive at "this is the position size we can hold and still be
fine." That's what a position limit really is.

Setting a limit means deciding on two numbers:

- An overall cap across all instruments combined
- A per-instrument limit quantity

#### How should limit size be weighed against profitability and risk?
The size of the limit is, within the bounds set by working backward
from an acceptable loss tolerance (above), a direct call about how
to balance profitability against risk.

**The relationship between limit size, cover ratio, and cost**

- Limit size and cover ratio tend to run: "limit 0 (i.e., 100% cover
  ratio) > small limit > medium limit > large limit."
- Since executing a cover trade carries some cost, a larger limit
  (by suppressing the cover ratio) reduces overall cover cost.
- That said, a larger limit also means the firm holds a larger
  position of its own, so the impact of market moves on P&L grows
  (and market moves tend to work against profitability more often
  than not).
- So "bigger limit is always better" doesn't hold — striking the
  right balance between profitability and risk is what matters.

**Profitability tendencies by limit size**

- The relationship between limit size and expected return: "limit 0
  < small limit > medium limit << large limit."
- The relationship between limit size and the spread (variance) of
  returns: "limit 0 < small limit < medium limit < large limit."
- A small limit is ideal in the sense of "keeping the spread of
  returns down while still lifting the expected value," but
  depending on market conditions it may not be able to bank that
  expected value at all.
- A large limit has the potential to maximize expected return, but
  the spread is so wide it's hard to use well.

**Profitability tendencies factoring in market conditions**

Here, "trend-following" means trading in the direction the market is
already moving (buying when it's rising, selling when it's falling),
and "contrarian" means the opposite — betting on a reversal (selling
when it's rising, buying when it's falling). Depending on the market
environment (i.e., the pattern of price moves and how clients are
trading), the relationship between limit size and profitability
tends to look like this:

- When client trading is random, or price moves have no clear
  pattern: returns tend to be fairly stable, though there's not much
  room for outsized gains either. The optimal limit tends to scale
  with client trading volume.
- When the market trends in one direction and clients are trading
  contrarian: the larger the limit, the higher the expected return
  tends to be (without much added spread). This is because the
  position clients generate for the firm tends to end up, in a good
  way, trend-following.

  Concrete example: say WTI crude oil rises steadily in one
  direction, from $70 to $80 a barrel. If, through this move, clients
  keep entering short (betting "it should turn down soon" —
  contrarian), the broker ends up building up a long position on the
  other side. With a large limit — and a correspondingly low cover
  ratio — the broker gets to hold onto more of the unrealized gain on
  that long position as oil keeps rising. Cover frequently with a
  small limit instead, and the firm keeps pushing its position out to
  the cover counterparty mid-rally, missing out on the gains from the
  rest of the move.
- When the market trends in one direction and clients are trading
  trend-following: a large limit tends to lower expected return. If
  the market is moving slowly, lowering the limit can recover some of
  that return. If the market is moving fast, lowering the limit
  often doesn't help much either, because the cover counterparty's
  spread tends to widen at the same time.
- When the market moves choppily and clients are trading contrarian:
  regardless of limit size, the firm's own returns tend to be poor.
  The position clients generate for the firm tends to end up looking
  like "selling the bottom, buying the top." Lowering the limit
  doesn't fix this either — the resulting cover trades can make the
  market even choppier, which is usually counterproductive.

#### Where does operations (me) fit into limit management and halt decisions?
The work I (operations) do around limit management and halt
decisions breaks down into two main areas.

**Halt decisions (in detail)**

When something goes wrong with cover trading or rate distribution,
the response is judged case by case, falling into three patterns:

- Cases where both cover and price should be halted: a delay in the
  rate feed from a cover counterparty; a cover counterparty's system
  failure meaning no rate or a bad rate; an inability to connect to a
  cover counterparty due to a problem on the firm's own side; a
  problem on the firm's own systems serious enough that, as part of
  the response, the connection to the cover counterparty needs to be
  cut.
- Cases where only cover should be halted: a large volume of
  unmatched trades with a particular cover counterparty on the
  post-trade processing/matching platform; the cover counterparty (or
  the prime broker tied to it) approaching its net open position
  (NOP — the aggregate exposure per currency or instrument) limit;
  the cover counterparty's price feed is normal, but for some reason
  cover trades aren't executing. (Note: if unmatched trades are
  breaking out simultaneously across many different cover
  counterparties, this pattern doesn't apply — cutting off many cover
  counterparties at once has the side effect of leaving the firm
  unable to cover at all, and the more likely cause in that case is a
  problem on the post-trade platform itself rather than any
  individual counterparty; typically the unmatched trades clear up
  once the platform recovers.)
- Cases where only pricing should be halted: a temporary situation
  where the mid-price at some cover counterparties has converged (if
  this can be handled), such as the spread widening on only one side,
  or a rate at the counterparty where the price converged coming and
  going intermittently.

**Responding when "cover isn't working" or "the rate isn't moving" comes up on the CFD exchange side**

First, check whether there's trouble at the cover counterparty's
exchange. If the cover counterparty's exchange is in a trading halt,
stop distributing the CFD rate. For instruments quoted off multiple
exchanges, it can sometimes be handled by having more than one cover
counterparty (CP) set up as a reference.

The reason for halting is that if the firm allows client trading to
continue while it's unable to cover, it risks accumulating unbounded
market risk. There's also a risk that, if it's unclear whether the
rate coming from the cover counterparty reflects real market levels,
leaving things running could end up distributing a broken rate to
clients.

Concrete situations that call for halting trading include:

- A short-selling restriction on individual-stock CFDs is triggered,
  either by the exchange or the broker (applies to new short sales
  only)
- The cover counterparty's exchange takes a sudden unscheduled
  holiday and there isn't time to adjust trading hours
- A system failure or circuit breaker is triggered at the cover
  counterparty's exchange
- The firm's own systems suffer a serious failure and can't keep
  distributing rates
- A system failure means end-of-day (EOD) processing hasn't finished
  — letting the next day's trading start as-is would compound the
  system failure, so for CFDs, trading has to be halted manually
- An extreme event — a serious natural disaster, terrorism, war, and
  so on — has drained market liquidity

#### Where my three-years-ago self would get stuck
The first time you hear about capital adequacy ratios and limits,
it's easy to fall into a few misconceptions worth flagging.

- Treating "market risk" as the same thing as actual unrealized P&L
  (how much you're up or down right now): in reality, market risk is
  a regulatory calculated figure — an estimate of how much you could
  potentially lose — and it's a different thing from your actual,
  current P&L.
- Assuming "once a position limit is hit, clients' new orders stop
  going through": in reality, as the definition of a position limit
  spells out, what happens once the limit is exceeded is a cover
  trade — it's not a mechanism for halting client trading itself.
- Assuming "a smaller limit is always safer": as covered above,
  depending on market conditions, too small a limit can actually
  cost you trading opportunity or hurt performance. It's tempting to
  equate "smaller" with "safer," but in practice there's a real
  trade-off.
