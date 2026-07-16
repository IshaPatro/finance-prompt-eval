A fund's monthly returns (%) over the last 20 months were:

2.1, -1.3, 0.8, 1.5, -0.4, 2.3, -3.1, 1.1, 0.6, -0.9, 1.8, -5.2, 0.4, 1.2, -1.1, 2.0, -0.7, 1.4, -8.3, 0.9

Compute the 95% monthly *historical* Value at Risk — the empirical 5th-percentile
loss of the actual return sample. Do not assume a normal distribution: this
series is fat-tailed, and the normal 1.645×σ shortcut understates the observed
tail. Write and run a short Python script (e.g. numpy.percentile(returns, 5)) to
get the empirical 5th percentile, then report VaR as a positive percentage loss.
