I'll write a Python script to compute the bond's current price, duration, convexity, and then estimate the price impact when rates rise 200bp.Perfect! Here's the complete analysis:

## Summary

**The estimated price change is approximately –19.86%** (from –23.81% without convexity adjustment to –19.86% with it).

### Key Findings

| Metric | Value |
|--------|-------|
| **Current Bond Price** (at 6% YTM) | $885.30 |
| **Macaulay Duration** | 12.62 years |
| **Modified Duration** | 11.90 |
| **Convexity** | 197.24 |
| | |
| **Duration Effect** (–MD × Δy) | –23.81% |
| **Convexity Effect** (½ × C × Δy²) | +3.94% |
| **Total Estimated Price Change** | **–19.86%** |
| **Absolute Price Change** | –$175.85 → $709.45 |

### Why Convexity Matters Here

- **Duration alone** would predict a price drop of 23.81%
- **Convexity adds back** 3.94 percentage points (a ~17% correction)
- **Net effect:** –19.86%

When rates rise, bond convexity works in the bondholder's *favor* by dampening price losses. For a 200bp move on a 20-year bond, this offset is **not optional**—it's material.

### Accuracy Check

The second-order approximation produces **–19.86%**, while the exact price calculation at 8% YTM gives **–20.31%**. The error is only **0.45%**, confirming the approximation is excellent for typical rate moves.

---

The script above computes all cash flows, builds the duration and convexity metrics from first principles, and demonstrates why a 20-year bond's curvature meaningfully reduces the price impact of a sharp rate rise.