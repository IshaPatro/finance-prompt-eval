# Finance prompt engineering

A small experiment in how much the *wording* of a prompt changes whether Claude
gets a finance question right.

Each of the six questions below has a well-known "shortcut" that sounds
reasonable but gives the wrong number. The **naive** prompts phrase the question
the way someone who doesn't know the gotcha would — and the model dutifully takes
the shortcut. The **guided** prompts spell out the correct method, and the model
lands on the right answer. Same question, same numbers, different framing.

---

## The six questions

| # | Question | Naive answer | Correct answer |
|---|----------|-------------|----------------|
| 01 | Average return of a fund over several years | Arithmetic mean → **2.24%** | CAGR (geometric) → **1.46%** |
| 02 | Sharpe ratio of a monthly return series | Raw mean / std → **0.20** | Risk-free-adjusted, annualised → **0.40** |
| 03 | Maximum drawdown of a price series | (high − low) / high → **23.65%** | Largest peak-to-trough drop → **19.83%** |
| 04 | Yield on a bond trading below par | Current yield → **5.64%** | Yield to maturity → **6.75%** |
| 05 | Annual interest rate on a loan | Quoted APR → **16.50%** | Effective annual rate → **17.81%** |
| 06 | Volatility of a 2-asset portfolio | Weighted average → **21.57%** | Correlation-adjusted → **19.13%** |

The naive answer is reliably wrong by more than the grading tolerance in every
case — the direction of the error is structural, not a rounding artefact.

---

## Why the naive prompts fail

### Q01 — Arithmetic mean vs CAGR

The naive prompt explicitly instructed: *"Just add up the yearly returns and
divide by the number of years."* The model followed that instruction exactly and
returned 2.24%.

The arithmetic mean is wrong here because it treats a −23.66% year the same as a
+23.66% year when computing the average, but compounding does not: a 50% loss
followed by a 50% gain leaves you at 75 cents on the dollar, not back to par.
The arithmetic mean always sits above the true compound rate whenever returns
vary, and the gap widens with volatility. With a year as bad as 2022 in the
series, the overstatement is meaningful — 0.78 percentage points here.

The fix was to name the correct method explicitly (CAGR), describe the geometric
chain, and warn that the simple average overstates compounded growth.

---

### Q02 — Raw mean/std vs annualised risk-adjusted Sharpe

The naive prompt said: *"Just take the mean of the monthly returns divided by
their standard deviation."* The model complied and returned 0.20.

This is wrong in two compounding ways. First, the Sharpe ratio is defined on
*excess* return — the numerator should be mean return minus the risk-free rate,
not the raw mean. Omitting the risk-free rate inflates the ratio. Second, the
result is on a monthly scale. Reporting it without annualising (×√12) makes it
incomparable to any standard benchmark. The correct annualised, risk-free-adjusted
Sharpe is 0.40 — half the naive figure.

The fix required three explicit instructions: subtract the monthly risk-free rate
from each return, divide mean excess return by its standard deviation, then
multiply by √12.

---

### Q03 — Global high/low vs peak-to-trough drawdown

The naive prompt specified: *"Take (highest value − lowest value) / highest
value."* The model applied the formula and returned 23.65%.

The error is temporal. In this price series the global high (117.58) is the
*last* data point — it comes months after the low (89.77). The naive formula
measures the distance between a trough and a peak that had not yet been reached
when the trough occurred. That is not a drawdown; it describes a rise. Maximum
drawdown requires tracking a running peak and measuring each subsequent dip from
the highest point reached *so far*. The true worst decline is 111.98 → 89.77,
giving 19.83%.

The fix was to describe the forward-walking running-peak algorithm and explicitly
state that the trough must come after the peak it is measured from.

---

### Q04 — Current yield vs yield to maturity

The naive prompt asked for *"the current yield: the annual coupon payment divided
by the current price."* The model computed 5.64% and stopped there.

Current yield counts only the coupon cash flows against the current price. It
ignores that a bond bought at a discount ($896.10 vs $1,000 face) will pay back
the full face value at maturity — that pull-to-par is real, taxable return. For
an 8-year bond the omission is large: the YTM is 6.75%, more than a full
percentage point above the current yield. The model was not wrong to compute what
the prompt asked; the prompt asked for the wrong thing.

The fix named YTM, required solving the full discounted cash flow equation in
coupon periods, and explicitly said: *"The coupon rate and the current yield are
not the answer."*

---

### Q05 — Quoted APR vs effective annual rate

The naive prompt framed the question as a confirmation: *"That's just the APR,
right? Confirm the annual rate as a percentage."* The model agreed and returned
16.50%.

APR is a nominal rate — it is the monthly rate multiplied by 12, which ignores
the interest-on-interest that accrues between periods. A borrower paying 1.375%
per month is not paying 16.50% per year in effective terms; the compounded cost
is (1 + 0.165/12)¹² − 1 = 17.81%. The confirmation framing of the naive prompt
primed the model to validate the user's assumption rather than challenge it.

The fix provided the EAR formula explicitly and stated that *"quoting the APR
back is wrong."*

---

### Q06 — Weighted average of vols vs correlation-adjusted portfolio vol

The naive prompt specified: *"Combine the two volatilities with the weights:
weightA × volA + weightB × volB."* The model returned 21.57%.

The weighted-average formula is the special case of the correct formula when the
two assets are perfectly correlated (ρ = 1). At any lower correlation the assets
partially offset each other — that is diversification — and the true portfolio
volatility falls below the weighted average. At ρ = 0.49 the benefit is a full
2.4 percentage points. The model was given a formula and used it; the formula was
wrong.

The fix supplied the correct expression including the cross-term
(2·wA·wB·ρ·σA·σB) and noted that the weighted average overstates risk whenever
ρ < 1.

---

## Layout

```
prompts/          bad_01..06.md  (naive)  +  good_01..06.md  (guided)
responses/        one file per prompt: the model's answer + metadata + verdict
responses/assets/ screenshots from the interactive Claude Code runs
metadata/         runs.json — machine-readable log of every run
```

---

## What gets recorded

Each run appends one record per prompt to `metadata/runs.json`:

```json
{
  "qid": "04",
  "category": "bad",
  "title": "Bond yield to maturity",
  "model": "claude-opus-4-8",
  "response_id": "msg_01...",
  "request_id": "req_01...",
  "timestamp_utc": "2026-06-30T13:57:26Z",
  "data_seed": 20260630,
  "extracted_answer": 5.6355,
  "correct_answer": 6.7522,
  "naive_answer": 5.6355,
  "tolerance": 0.1,
  "is_correct": false,
  "prompt_file": "prompts/bad_04.md",
  "response_file": "responses/bad_04.md"
}
```

The responses in `responses/` were produced by pasting prompts into an
interactive Claude Code session. Because of that, `response_id` and `request_id`
are marked `n/a` — those fields are only populated when the Messages API is used
directly.
