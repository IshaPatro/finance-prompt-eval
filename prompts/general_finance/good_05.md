A European call option has a strike price of $100 and expires in one year. The
underlying stock trades at $108 today, the risk-free rate is 5% per year, and the
stock's volatility is 30% per year.

Price the option with the Black-Scholes formula for a European call,
C = S·N(d1) − K·e^(−rT)·N(d2), where d1 = [ln(S/K) + (r + σ²/2)·T] / (σ·√T),
d2 = d1 − σ·√T, and N(·) is the standard normal CDF. Intrinsic value alone is
wrong because it ignores the option's time value — the chance the stock rises
further before expiry while the downside stays capped at zero. There's no
mental-math shortcut for the normal CDF, so write and run a short Python script to
compute it. Report the option's value in dollars.
