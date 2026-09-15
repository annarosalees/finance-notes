# CFD Notes

🇯🇵 [日本語版](./cfd.md)

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
