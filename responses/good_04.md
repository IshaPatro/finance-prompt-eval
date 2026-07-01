# good_04 - Bond yield to maturity (guided prompt)

- model: claude-opus-4-8
- run_type: interactive Claude Code chat
- response_id: n/a  (see note)
- request_id: n/a  (see note)
- timestamp_utc: 2026-06-30T14:21:14Z
- data_seed: 20260630  (prompts generated for 2026-06-30)
- extracted_answer: 6.7522%
- correct_answer: 6.7522%   |   naive_answer: 5.6355%
- tolerance: 0.1%
- verdict: CORRECT
- note: interactive Claude Code chat run — the prompt was answered by the model in the session, not through the Messages API, so Anthropic response_id / request_id are not issued. Run `python run.py run` to capture those automatically.

## Prompt

A bond has a face value of $1,000, an annual coupon rate of 5.05%
paid semiannually, 8 years to maturity, and currently trades at $896.10.

Find its yield to maturity (YTM) — the discount rate that makes the present
value of every coupon payment plus the face value repaid at maturity equal the
current price. Work in coupon periods, not years: the per-period coupon is
face_value × coupon_rate / 2, and there are 8 × 2 periods. Solve for the
per-period rate numerically (there's no closed form), then annualize it by
multiplying by 2 to get the bond-equivalent yield. The coupon rate and the
current yield are not the answer. Report the YTM as a percentage.

## Model response

Yield to maturity — the rate that discounts all cash flows back to the price.

Working in semiannual periods:
  coupon per period = 1,000 × 5.05% / 2 = 25.25
  number of periods = 8 × 2 = 16
  price = 896.10, redemption = 1,000 at period 16

Solve for the per-period rate y in:
  896.10 = Σ_{t=1..16} 25.25/(1+y)^t + 1000/(1+y)^16
  → y = 3.3761% per period

Bond-equivalent yield = 3.3761% × 2 = 6.7522%

**YTM ≈ 6.75%.** Above the coupon rate (5.05%) and current yield (5.64%) because
the bond trades at a discount and pulls to par at maturity.
