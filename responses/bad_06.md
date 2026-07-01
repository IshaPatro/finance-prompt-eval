The weighted average you specified gives **21.57%**, but that formula overstates the portfolio's volatility, and here the gap is a full 2.4 points — because it silently assumes the two assets move in perfect lockstep, which at a correlation of 0.49 they don't.

Volatilities don't add linearly the way expected returns do. The correct combination squares the weighted vols and adds a cross term scaled by the correlation:

σ_p = √(w²ₐσ²ₐ + w²ᵦσ²ᵦ + 2·wₐ·wᵦ·ρ·σₐ·σᵦ) = **19.13%**.

The weighted average is actually the special case of this formula when ρ = 1. Any correlation below 1 means the assets partially offset each other — that's diversification — and pulls the portfolio vol below the weighted average. At ρ = 0.49 the benefit is meaningful: 19.13% versus 21.57%. Only if the two assets were perfectly correlated would your 21.57% be right, and it marks the upper bound the true figure can never exceed.

So the portfolio's annualized volatility is **19.13%**.