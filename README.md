# Lab 3: Volatility Estimation, Value at Risk (VaR), and Scenario Analysis

## Submission - November 19th, 2026 (EOD)

## Objective

The objective of this lab is to estimate and compare different measures of stock price volatility, calculate daily Value at Risk (VaR) using multiple methods, and examine how estimated financial risk changes under different market scenarios.

The emphasis is on **understanding the methods, interpreting the results, and identifying their practical advantages and limitations**, rather than simply implementing formulas.

## Task 1: Stock Selection and Justification

Select **one reasonably liquid Indian stock** listed on the NSE or BSE.

- Choose a company that interests you, perhaps one that has recently been in the news or experienced interesting market movements.
- Briefly explain why you selected this stock.
- Justify its liquidity using at least one liquidity measure discussed in class.

Using `yfinance`, download daily adjusted closing prices for your stock and compute **daily simple returns in decimal form**, $r_t = \frac{P_t - P_{t-1}}{P_{t-1}}$, as in the sample notebook. Use simple (not log) returns throughout the lab, and keep all volatility and VaR estimates on a **daily** basis (not annualised).

> **Note on sample length:**
> - **Volatility estimation (Task 2)** requires a **longer history** (e.g. several years, as in the sample notebook), because rolling windows of up to 200 days and GARCH estimation need many observations before they produce meaningful estimates.
> - **VaR calculations (Tasks 3-6)** use only the **most recent 200 trading days of daily returns**.

**Report Deliverables:**
- Stock name, ticker, and brief justification for selection.
- Liquidity measure(s), including the calculation and interpretation.
- Data periods (for both the volatility-estimation sample and the 200-day VaR sample) and any relevant assumptions.

## Task 2: Volatility Estimation and Analysis

Refer to the provided **`volatility_sample.ipynb` notebook**, which demonstrates rolling historical volatility, EWMA, and GARCH(1,1) estimation.

Use the notebook as a starting point, modifying and extending it as you consider appropriate for your selected stock. You are encouraged to experiment with different **estimation windows, decay factors, model parameters, and specifications**.

Using your longer return history (see the note in Task 1):

1. Estimate the different volatility measures.
2. Plot and compare their behavior over time.
3. Examine periods where the estimates behave similarly, diverge, or exhibit unusual changes.

**Consider the following questions:**

- Which volatility measures react most quickly to recent market movements?
- Are there noticeable volatility spikes or periods of relative stability?
- How do different estimation windows or parameter choices affect the results?
- Under what market conditions might one volatility estimator be more appropriate than another?

**Report Deliverables:**
- Relevant volatility plots and comparison figures.
- Assumptions, parameter choices, and justifications for any modifications.
- Observations and interpretations of noticeable patterns, differences, and volatility movements.
- Potential advantages, disadvantages, and suitability of the different estimators.

## Task 3: Historical VaR

Calculate **one-day VaR at 90%, 95%, and 99% confidence levels** using historical data.

**Method:**

1. Calculate the daily returns of your selected stock.
2. Construct the empirical distribution of the 200 historical daily returns.
3. Identify the appropriate lower-tail percentile for each confidence level:
   - 90% VaR: 10th percentile.
   - 95% VaR: 5th percentile.
   - 99% VaR: 1st percentile.
4. Express VaR as a positive loss percentage.

For example, if the 5th percentile of historical returns is -2.5%, the estimated 95% daily VaR is 2.5%.

**Report Deliverables:**
- A table containing all three VaR estimates.
- Any relevant assumptions or methodological choices.
- Observations and interpretations, including the potential advantages and disadvantages of historical simulation.

## Task 4: Parametric VaR

Calculate **one-day parametric VaR at 90%, 95%, and 99% confidence levels** using the normal-distribution formula discussed in class.

Use two different volatility estimates:

**1. Historical Volatility**

Select a historical volatility estimation window of your choice, up to 200 trading days. Justify your selection.

**2. EWMA or GARCH Volatility**

Use the latest one-day-ahead volatility estimate from either EWMA or GARCH

**Report Deliverables:**
- A table containing all **six VaR estimates** (three confidence levels × two volatility measures).
- Estimation windows, parameters, assumptions, and their justifications.
- Interesting differences or patterns in the results, with possible explanations.
- Potential advantages and disadvantages of parametric VaR and the chosen volatility estimators.

## Task 5: Monte Carlo VaR

Calculate **one-day VaR at 90%, 95%, and 99% confidence levels** using Monte Carlo simulation.

Monte Carlo simulation generates a large number of possible next-day returns using a probability distribution whose parameters are estimated from historical data.

A general simulation model is:

$$
R_{t+1} = \mu_d + \sigma_d Z
$$

where $\mu_d$ and $\sigma_d$ are the estimated daily expected return and volatility, while $Z$ is drawn from a chosen standardized probability distribution.

**Suggested procedure:**

1. Use the 200 historical daily returns to estimate the expected daily return and volatility.
2. Select a probability distribution for returns (e.g., Student-t, Normal, etc). This determines how the random variable $Z$ is generated.
3. Generate at least 10,000 simulated next-day returns using the model above.
4. Obtain VaR from the 10th, 5th, and 1st percentiles of simulated returns, expressing VaR as a positive loss percentage.

Ensure that the chosen distribution is appropriately parameterized.

**Report Deliverables:**
- A table containing the three Monte Carlo VaR estimates.
- Historical parameters used, chosen distribution, number of simulations, and justification of assumptions.
- Observations and interpretations, particularly differences from historical and parametric VaR.
- Potential advantages, disadvantages, and limitations of Monte Carlo VaR.

## Task 6: VaR Comparison and Scenario Analysis

### Part A: Comparison of VaR Methods

Prepare a single comparison table containing all VaR estimates from Tasks 3-5.

| Method | 90% VaR | 95% VaR | 99% VaR |
|---|---|---|---|
| Historical Simulation | | | |
| Parametric - Historical Volatility | | | |
| Parametric - EWMA/GARCH | | | |
| Monte Carlo Simulation | | | |

**Discuss:**

- Which methods produce higher or lower VaR estimates? Why?
- How do the volatility estimators and distributional assumptions affect the results?
- What similarities, differences, or unusual patterns do you observe?
- Which method would you consider most appropriate for your selected stock, and why?

### Part B: Parametric VaR Scenario Analysis

Using **the historical volatility based parametric VaR models from Task 4**, construct a two-dimensional scenario table showing how changes in expected daily return and daily volatility affect VaR.

Use **95% one-day VaR** throughout this exercise.

**Procedure:**

1. Select the historical volatility based parametric VaR.
2. Use the expected daily return and daily volatility from the selected model as the baseline.
3. Consider different hypothetical changes in expected daily returns and volatility relative to their baseline values.
4. Recalculate VaR for every combination using the parametric VaR formula.
5. Present the results in a two-dimensional scenario table, preferably as a heatmap. (Eg. On one axis, change the value of the expected returns relative to the baseline values, on the other axis, change the value of the volatility relative to the baseline values).

The **Baseline–Baseline cell must reproduce the 95% parametric VaR** obtained using your selected model in Task 4.

**Discuss:**

- How does VaR change when expected daily returns become more negative or positive?
- How does VaR respond to increasing or decreasing volatility?
- Which combination of assumptions produces the highest estimated risk?
- What does this analysis suggest about the sensitivity and limitations of parametric VaR?
- Can you identify any plausible market conditions for your selected company that might resemble these hypothetical scenarios?

**Report Deliverables:**
- Completed two-dimensional scenario table or heatmap.
- Observations and interpretations of changing risk across scenarios.
- Brief discussion of the practical relevance and limitations of the scenario analysis.

---

## Submission Instructions

Submit the following **two files**:

### 1. Jupyter Notebook (`.ipynb`)

A single, complete, executable notebook containing:

- Data retrieval and preprocessing.
- Volatility estimation and plots.
- All VaR calculations and Monte Carlo simulations.
- Comparison tables and scenario analysis.

Organize the notebook according to the six tasks. You may reuse, modify, and extend the provided `volatility_sample.ipynb` notebook.

### 2. Brief Report (`.pdf`)

The report should contain the requested **deliverables for each task**, with particular emphasis on:

- Assumptions, parameter choices, and their justifications.
- Relevant calculations (such as liquidity measures), result tables, and plots.
- Observations and interpretations of the findings.
- Notable patterns, differences, and possible explanations.
- Advantages, disadvantages, and limitations of the various approaches.

**The objective is not to identify a universally superior model, but to understand how different volatility measures, VaR methodologies, and market assumptions influence estimates of financial risk.**
