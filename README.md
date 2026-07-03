# Finance prompt engineering

A small experiment in how much a prompt's *wording* changes whether Claude gets a
finance question right. Each of the six questions has a plausible-sounding
shortcut that produces the wrong number. The **naive** prompt phrases the question
the way someone who doesn't know the gotcha would, and the model takes the
shortcut; the **guided** prompt names the correct method, and the model gets it
right.

## The six questions

| # | Question | Naive answer | Correct answer |
|---|----------|-------------|----------------|
| 01 | Average return of a fund over several years | Arithmetic mean → **2.24%** | CAGR (geometric) → **1.46%** |
| 02 | Sharpe ratio of a monthly return series | Raw mean / std → **0.20** | Risk-free-adjusted, annualised → **0.40** |
| 03 | 95% Value at Risk of a return series | Normal 1.645×σ → **4.38%** | Historical 5th percentile → **5.36%** |
| 04 | Yield on a bond trading below par | Current yield → **5.64%** | Yield to maturity → **6.75%** |
| 05 | Value of a one-year European call option | Intrinsic value → **$8.00** | Black-Scholes → **$19.61** |
| 06 | Return on a multi-fund portfolio | Simple average → **8.00%** | Dollar-weighted → **6.00%** |

Every naive answer is wrong by a structural margin, not a rounding artefact.

## Why the naive prompts fail

- **Q01 — Arithmetic mean vs CAGR.** Averaging the yearly returns gives 2.24%, but
  a plain average ignores compounding; one −23.66% year drags the true geometric
  return (CAGR) down to 1.46%.
- **Q02 — Sharpe ratio.** Raw mean ÷ std gives 0.20. A proper Sharpe uses *excess*
  return (minus the risk-free rate) and is annualised (×√12) → 0.40.
- **Q03 — Value at Risk.** The normal shortcut 1.645×σ gives 4.38%, but the series
  has a fat left tail, so the historical 5th percentile (`numpy.percentile`) is
  deeper at 5.36%.
- **Q04 — Bond yield.** Current yield (coupon ÷ price) is 5.64% but ignores the
  pull-to-par on a discount bond; yield to maturity is 6.75%.
- **Q05 — Option value.** Intrinsic value is $8, but a call with a year left also
  has time value. The naive prompt omits volatility and the risk-free rate, so the
  shortcut is all it can compute; Black-Scholes (given σ = 30%, r = 5%) prices it
  at $19.61.
- **Q06 — Portfolio return.** Averaging the three funds' returns gives 8.0%, but a
  portfolio is dollar-weighted; the $5,000 position at 2% pulls the real return
  down to 6.0%.

For the heavier calculations (Q03 and Q06) the guided prompt has the model write
and run a short Python script to reach the exact figure.

## Layout

```
prompts/          bad_01..06.md (naive) + good_01..06.md (guided)
responses/        one markdown file per prompt — the model's answer
responses/assets/ screenshots from the interactive Claude Code runs
metadata/         runs.json — per-run log (answers, verdict, metadata)
```

## What gets recorded

Each prompt has one record in `metadata/runs.json`:

```json
{
  "qid": "04",
  "category": "bad",
  "title": "Bond yield to maturity",
  "model": "claude-opus-4-8",
  "response_id": null,
  "request_id": null,
  "timestamp_utc": "2026-06-30T14:21:14Z",
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

`response_id` and `request_id` are `null` because the answers came from an
interactive Claude Code session rather than the Messages API. `data_seed` fixes
the generated parameters so a run is reproducible.
