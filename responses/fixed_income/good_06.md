## Yield to Maturity (YTM)

Set up the equation with 20 semiannual periods and $1,000 redemption:

$$1,080 = \sum_{t=1}^{20} \frac{35}{(1+r)^t} + \frac{1,000}{(1+r)^{20}}$$

Testing $r = 0.02945$ (semiannual):
- PV of coupons: $35 × 14.813 = $518.46
- PV of face: $1,000 / 1.7776 = $562.64
- **Total: $1,081.10** ✓

**Annualized YTM: 0.02945 × 2 = 5.89%**

## Yield to Call (YTC)

Set up the equation with 8 semiannual periods and $1,020 call price:

$$1,080 = \sum_{t=1}^{8} \frac{35}{(1+r)^t} + \frac{1,020}{(1+r)^8}$$

Testing $r = 0.0265$ (semiannual):
- PV of coupons: $35 × 7.1139 = $249.00
- PV of call price: $1,020 / 1.2250 = $832.65
- **Total: $1,081.65** ✓

**Annualized YTC: 0.0265 × 2 = 5.30%**

## Yield to Worst

The bond trades at a $80 premium above the call price. The issuer will likely call it in 4 years, limiting the investor's upside. Therefore:

$$\text{Yield to worst} = \min(5.89\%, 5.30\%) = \boxed{5.30\%}$$

**Source: Yield to Call**

A buyer paying $1,080 should expect to earn only 5.30% annually, not the 5.89% promised to maturity—because the bond will almost certainly be called away at $1,020 in 4 years.