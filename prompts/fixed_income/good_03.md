We hold two U.S. Treasury STRIPS (zero-coupon, single cash flow each):

- STRIP A: pays $10,000 in exactly 1 year, currently priced at $9,708.74
- STRIP B: pays $10,000 in exactly 2 years, currently priced at $8,734.39

Find the 1-year forward rate for year 2 — the rate f that makes rolling STRIP
A's return and then reinvesting at f for year 2 equal to holding STRIP B
outright:

1. Get STRIP A's implied 1-year rate r1 from $10,000 / $9,708.74.
2. Get STRIP B's implied 2-year *compounded* rate r2 from ($10,000 /
   $8,734.39)^(1/2) — not a simple average or a straight-line annualization.
3. Solve (1 + r2)² = (1 + r1) × (1 + f) for f.

Don't approximate step 2 by dividing STRIP B's total gain evenly across the two
years — that's simple interest and understates the compounding, which throws
off the forward rate. Report f as a percentage.
