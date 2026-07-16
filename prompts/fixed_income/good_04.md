A bond has these cash flows: a 5% annual coupon ($50) on a $1,000 face value,
paid once a year for 20 years, plus the $1,000 face value returned at year 20.
It currently yields 6% to maturity.

Rates are about to rise by 200 basis points (Δy = +0.02). Estimate the price
impact properly, in two steps:

1. From the cash flows, compute the bond's price at the current 6% yield,
   its Macaulay duration (Σ t·PV(CFₜ) / Price), modified duration
   (Macaulay / (1+y)), and convexity (Σ t(t+1)·PV(CFₜ) / (Price·(1+y)²)).
2. Estimate the price change with the second-order approximation:
   %ΔPrice ≈ −(modified duration × Δy) + ½ × convexity × Δy².

A 20-year bond has enough curvature that duration alone materially overstates
the price drop on a 200bp move — the convexity term is not optional here. Write
and run a short Python script to do the cash-flow arithmetic, and report the
estimated percentage price change.
