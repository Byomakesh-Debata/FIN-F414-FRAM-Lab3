# Lab 2 - Volatility Estimation and Comparison

## Submission Deadline - EOD, 20 September, 2026

## Purpose of the Lab

The objective of this lab is to compare different methods of estimating volatility and examine whether their behaviour varies across Indian stocks with different industry and liquidity characteristics.

The lab covers:

1. Rolling historical volatility
2. Exponentially Weighted Moving Average (EWMA) volatility
3. GARCH volatility models

Before beginning, read **Chapter 23: Estimating Volatilities and Correlations** from *Options, Futures, and Other Derivatives*, 11th Edition, by John C. Hull. You may also consult any additional readings or sources to understand this better.

## Instructions

### Step 1: Study the reference material

Read the prescribed chapter and supporting material to understand:

- How historical, EWMA and GARCH volatility are calculated.
- How recent and older observations are weighted.
- The strengths and limitations of each method.

### Step 2: Study the sample notebook

Go through the sample volatility notebook carefully.

Understand:

- How prices and log returns are prepared.
- How daily volatility is annualised.
- How rolling historical volatility is calculated.
- How EWMA and GARCH(1,1) are implemented.
- Why ARCH effects are tested before estimating GARCH.
- How the volatility estimates are compared graphically.

The sample notebook presents only one possible approach (there can be multiple ways to implement the same model). You may modify the code, parameters and model specifications where appropriate.

### Step 3: Select six Indian stocks

Select six Indian-listed stocks (other than the example showcased in the sample notebook) from different industries and with different liquidity characteristics. Use the same sample period and data frequency for every stock.

Justify:

1. The industries selected.
2. The company selected within each industry.
3. The differences in liquidity across the selected stocks.
4. Why volatility behaviour might differ across these companies or industries.

Calculate at least one liquidity measure

You may use additional liquidity measures if properly explained.

### Step 4: Estimate volatility

For each company, calculate:

1. Rolling historical volatility.
2. EWMA volatility.
3. GARCH volatility.

Use the same basic specifications across companies initially to make the results comparable. You may then vary:

- Historical-volatility window length.
- EWMA decay factor, $\lambda$.
- GARCH lag orders
- Sample period or other relevant modelling choices.

Use an ARCH-effects test before fitting a GARCH model.

Clearly state the formulas, parameter values and annualisation convention

### Step 5: Compare the results

For every company, include:

1. A historical return plot.
2. Historical-volatility plots.
3. EWMA-volatility plots.
4. GARCH-volatility plots.
5. A combined comparison of the volatility estimates.

Examine:

- How quickly each measure responds to return shocks.
- How long elevated volatility persists.
- The effect of changing the historical window or EWMA decay factor.
- Whether volatility clustering is present.
- Whether GARCH is suitable for the return series.
- Whether the three methods produce materially different estimates.
- How the results differ across industries and liquidity levels.

Do not assume that one method is universally superior. Explain what the graphs and model results can and cannot establish.

## Report

The report should contain:

1. A brief description of the data and methodology.
2. A table describing the six companies, industries and liquidity measures.
3. Justification for each company’s inclusion.
4. Return and volatility plots for every company.
5. Interpretation of the results for each company.
6. Comparison across companies, industries and liquidity levels.
7. Discussion of the effect of changing model parameters.
8. Limitations of the analysis.
9. A short conclusion.

Interpretations must be written in your own words. Focus on the patterns you observe and explain why they may arise. Do not merely describe whether a line moves upward or downward.

## Final Deliverables

Submit the following two files:

1. One `.ipynb` notebook containing the complete analysis for all six companies.
2. One report in PDF format containing the relevant plots, results and interpretations.