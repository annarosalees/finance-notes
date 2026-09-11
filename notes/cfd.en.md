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
