## Step 1: Calculate Macaulay Duration

I need to find the weighted average time to receive all cash flows, discounted at 6%:

**Bond price at 6% yield:**
- PV of coupons = $50 × [1 - (1.06)^-20] / 0.06 = $50 × 11.470 = $573.50
- PV of face value = $1,000 / (1.06)^20 = $1,000 / 3.2071 = $311.80
- **Total price = $885.30**

**Macaulay duration** (weighted sum of discounted cash flows divided by price):

$$D_{mac} = \frac{\sum_{t=1}^{20} t \cdot \frac{50}{(1.06)^t} + 20 \cdot \frac{1,000}{(1.06)^{20}}}{885.30}$$

Computing the weighted sum:
- Years 1-20 coupons: $4,933.10 (calculated by weighting each coupon by its year)
- Year 20 face value: 20 × $311.80 = $6,236.00
- **Total weighted sum = $11,169.10**

$$D_{mac} = \frac{11,169.10}{885.30} = 12.62 \text{ years}$$

## Step 2: Convert to Modified Duration

$$D_{mod} = \frac{D_{mac}}{1 + y} = \frac{12.62}{1.06} = \boxed{11.91}$$

## Step 3: Apply Duration Linearly

$$\%\Delta \text{Price} = -(D_{mod} × \Delta y) = -(11.91 × 0.02) = \boxed{-23.82\%}$$

**Estimated percentage price change: −23.82% (or approximately −23.8%)**

A 200 basis point rate increase causes the bond price to drop by roughly 24%, reflecting the bond's high duration (typical for a long-term, low-coupon bond trading at a discount).