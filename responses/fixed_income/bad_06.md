## Setting Up the YTM Equation

For a bond with semiannual coupons, the price equals the present value of all cash flows:

$$1,080 = \sum_{t=1}^{20} \frac{35}{(1+r)^t} + \frac{1,000}{(1+r)^{20}}$$

where:
- $35 = semiannual coupon (7% annual ÷ 2)
- 20 = number of periods (10 years × 2)
- $r$ = semiannual discount rate (unknown)

## Solving for the Semiannual Yield

This requires numerical methods (trial-and-error, financial calculator, or spreadsheet). Testing values:

At $r = 0.02945$ (2.945% semiannual):
- PV of coupons: $35 × 14.813 = $518.46$
- PV of face: $1,000 / 1.7776 = $562.64$
- **Total: $1,081.10** ✓ (very close)

## Annualizing the Yield

$$\text{Annual YTM} = 0.02945 × 2 = \boxed{5.89\%}$$

## Important Note on Callable Bonds

This bond trades at **$1,080, which is above the call price of $1,020**. The issuer is likely to call it in 4 years if rates fall or remain stable. In that case, the investor won't receive the full 10-year cash flows, and the actual return will be lower than the YTM.

The more relevant yield measure is the **yield to call (YTC)**, which discounts cash flows to the call date (4 years) and the call price ($1,020), not to maturity. For a bond trading above its call price, YTC is typically lower than YTM and more predictive of actual return.

**Yield to maturity: 5.89%**