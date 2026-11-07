# Dollar Strength vs. Luxury Stocks

**Author:** Antonia Velasquez

**Status:** Version 2 (monthly data, 2019–2026). Version 1 (annual data) is kept in `analysis/`.

**Dashboard:** [https://public.tableau.com/app/profile/antonia.velasquez/viz/DollarStrengthvs_LuxuryStocks/DollarStrenthvs_LuxuryStocks]

## Question
When the dollar weakens against the euro, does LVMH's stock price tend to fall? And is the dollar's link with luxury stocks specific to luxury, or a market-wide pattern?

## Hypothesis
A stronger euro makes LVMH's foreign earnings worth less when converted into euros, so LVMH's stock should tend to fall when the dollar weakens.

## Data
- **Broad U.S. Dollar Index (DTWEXBGS)** and **U.S. dollars per euro (DEXUSEU):** FRED, Federal Reserve Bank of St. Louis (fred.stlouisfed.org).
- **Stock prices (daily close):** Google Finance, via the GOOGLEFINANCE function in Google Sheets: LVMH (EPA:MC), Hermès (EPA:RMS), Kering (EPA:KER), Ralph Lauren (NYSE:RL), Tapestry (NYSE:TPR), and the S&P 500 as a market benchmark.
- **Period:** January 2019 – October 2026. Monthly values are the last available daily value of each month (93 monthly % changes). October 2026 is incomplete, and its last available date differs by series (FRED: Oct 23; LVMH: Oct 27; other stocks and the S&P 500: Oct 30).

### Data note
The stock price data belongs to its original providers and is included here only for educational, non-commercial use. If you are a rights holder and would like it removed, please contact me and I will take it down.

## Method
1. Cleaned the data in Excel (removed days without values: 213 in Broad, 281 in EUR).
2. Took month-end values with XLOOKUP and calculated monthly % changes.
3. Measured correlation, R-squared, slope and p-values.
4. Added robustness checks (excluding 2020; from January 2022 onward).
5. Compared LVMH with Hermès and Kering (euro reporters), Ralph Lauren and Tapestry (dollar reporters), and the S&P 500.
6. Removed the market component two ways: subtracting the S&P 500's change, and subtracting beta × the S&P 500's change.

## Results

[Dashboard](images/Dashboard.png)

**1. The claim "the dollar is at its lowest since 2019" does not hold in this data.** The broad index was lowest in May 2021 (110.76) versus 121.32 in late October 2026; USD per EUR peaked in December 2020 (1.223) versus 1.12.

**2. LVMH vs. the dollar (n = 93 monthly changes).**

| Series | r | R² | p-value |
|---|---|---|---|
| USD per EUR vs. LVMH | 0.091 | 0.008 | 0.386 |
| Broad index vs. LVMH | -0.273 | 0.075 | 0.008 |

The broad-index link weakens excluding 2020 (r = -0.204, p ≈ 0.07) and from 2022 onward (r = -0.181, p ≈ 0.17).

**3. Comparison group: correlation with the broad dollar index.**

| Company | Reports in | Raw | Market-adjusted | Beta-adjusted |
|---|---|---|---|---|
| LVMH | EUR | -0.273 | 0.111 | 0.070 |
| Hermès | EUR | -0.260 | 0.101 | 0.042 |
| Kering | EUR | -0.287 | -0.014 | -0.006 |
| Ralph Lauren | USD | -0.431 | -0.223 | -0.069 |
| Tapestry | USD | -0.428 | -0.259 | -0.140 |
| S&P 500 | USD | -0.586 | n/a | n/a |

**Reading:** all five luxury stocks tend to fall when the dollar strengthens, but the S&P 500 does so even more strongly. After adjusting for each stock's beta, none of the ten correlations with the dollar is statistically significant.

**Conclusion:** I found no evidence that a weaker dollar lowers LVMH's price through currency translation. The dollar's apparent link with luxury stocks looks like a market-wide pattern. Not finding evidence is not proof that no effect exists.

## Limitations
- Correlation does not show causation.
- With 93 observations, a correlation needs to be about 0.20 in absolute value to be significant at 5%, so a small real effect could go undetected.
- Ten tests were run; p-values near 0.05 are suggestive, not conclusive.
- The five luxury stocks are from the same sector and are not independent.
- Beta was estimated over the whole period.
- Ralph Lauren, Tapestry and many S&P 500 companies also earn income abroad.
- European and U.S. markets close at different times.
- October 2026 is incomplete.

## How to reproduce the stock data
In Google Sheets, in cell A1:

`=GOOGLEFINANCE("EPA:MC","close",DATE(2019,1,1),TODAY(),"DAILY")`

Replace `EPA:MC` with the ticker you need. If your regional settings show an error, replace the commas with semicolons. Prices may change slightly over time.

## Files
- `analysis/dollar-lvmh-analysis-v2.xlsx`: full workbook (data, formulas, results, notes)
- `analysis/dollar-lvmh-analysis-v1.xlsx`: version 1 (annual data)
- `data/raw/`: original FRED downloads
- `images/`: charts and dashboard screenshot

## Next steps
- Repeat with longer history (FRED data go back to 1999/2006)
- Add Python analysis (rolling correlations)
- Test other luxury companies and currencies

## Disclaimer
This is a student learning project, not investment advice.
