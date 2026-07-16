The funds hold different dollar amounts, so the portfolio's return is the
dollar-weighted average of the three returns, not the plain average.

```python
holdings = [(5000, 2), (3000, 6), (2000, 16)]
total = sum(v for v, _ in holdings)
weighted = sum(v * r for v, r in holdings) / total
print(round(weighted, 2))
```

Output: `6.0`

**Portfolio return: 6.0%.**

Half the money sits in Fund A at just 2%, so that position dominates. Weighting by
dollars, Fund A contributes 0.5 × 2 = 1.0%, Fund B 0.3 × 6 = 1.8%, and Fund C
0.2 × 16 = 3.2% — totaling 6.0%. The equal-weighted average overstates the result
at 8.0% because it treats the small 16% position as if it were as large as the
2% one.
