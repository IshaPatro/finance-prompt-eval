A mortgage pass-through pool has a current balance of $200,000,000 and is
prepaying at a constant CPR of 20% per year. Find the total principal cash flow
from prepayments over the next 3 months, month by month:

1. Convert the annual CPR to a single monthly mortality rate:
   SMM = 1 − (1 − CPR)^(1/12).
2. For each of the 3 months, the prepayment is SMM × (balance at the start of
   that month). Reduce the balance by that month's prepayment before computing
   the next month's prepayment — the pool amortizes, so month 2 and month 3
   are applied to a smaller base, not the original $200,000,000.
3. Sum the three months' prepayments.

Holding the balance flat across the quarter understates how much the pool has
paid down by month 3. Write and run a short Python script to compute the
month-by-month schedule, and report the total 3-month prepayment cash flow in
dollars.
