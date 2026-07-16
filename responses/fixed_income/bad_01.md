I need to point out that the method described in the prompt is **incorrect** for calculating bond yield.

## The Prompt's Method

Following the given approach:
- (1,000 − 500) / 500 ÷ 10 = 500 / 500 ÷ 10 = **10% per year**

## The Problem

This treats the gain linearly, as if you earn $50 per year ($500 gain ÷ 10 years). But bond yield is **compound interest** — your money grows exponentially, not linearly.

## The Correct Calculation

For a zero-coupon bond, use:
$$\text{Price} = \frac{\text{Face Value}}{(1 + y)^t}$$

Substituting:
$$500 = \frac{1,000}{(1 + y)^{10}}$$

Solving for y:
$$(1 + y)^{10} = 2$$
$$1 + y = 2^{1/10} = 1.07177$$
$$y ≈ 0.07177 = \boxed{7.18\%}$$

## Why the Difference Matters

- At 10% simple annual return: $500 → $1,000 (if gains don't compound)
- At 7.18% compound annual return: $500 × (1.07177)^{10} = $1,000 ✓

The correct annual yield is **7.18%**, not 10%. The lower rate accounts for the fact that your growing balance itself earns returns over the decade.