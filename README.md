# portfolio-simulation-monte-carlo

Monte Carlo simulation on various portfolios.

Based on the provided portfolio securities and theirs weights, the code calculates outcomes of Monte Carlo simulation. It converts all data to a specified **analysis currency** to facilitate the analysis.

It is mainly intended for portfolios consisting of ETFs (Exchange Traded Funds). Therefore, I will use ETFs in examples below.

The data for analysis comes from Yahoo Finance, and it is retrieved using the yfinance library.

## Table of contents

1. [Overview](#Overview)
2. [Analysed results](#Analysed-results)
3. [Visualizations](#Visualizations)
4. [Simulation parameters](#Simulation-parameters)
5. [Examples](#Examples)

## Overview

Monte Carlo simulation is a statistical technique that allows for the modeling of the probability distribution of different outcomes in a process that cannot easily be predicted due to the presence of random variables.

In the context of portfolio management, Monte Carlo generates a range of different scenarios based on randomly generated input data, such as asset prices, transaction quantities, etc. For each scenario, financial outcomes, such as profits and losses are calculated. By analyzing the set of results, a more realistic assessment of the potential investment outcomes can be obtained, taking into account the diversity of possible market conditions

## Analysed results

### Profit statistics

#### Profits for each iteration

- **Description:** A dictionary containing statistics of profit for each iteration.
- **Variable:** `results_profit_describe`
- **Usage:** This dictionary provides a comprehensive overview of the profit statistics observed in each simulation iteration.

#### Profit percentage for each iteration

- **Description:** A dictionary with statistics of profit percentage for each iteration.
- **Variable:** `results_profit_percentage_describe`
- **Usage:** This dictionary captures the percentage change in profit for each simulation iteration, offering insights into relative performance.

### Drawdown statistics

#### Drawdown for each iteration

- **Description:** A dictionary with statistics of drawdown for each iteration.
- **Variable:** `results_drawdown_describe`
- **Usage:** This dictionary provides insights into the depth of decline from a peak in the value of the portfolio for each simulation iteration.

### CAGR statistics

#### Compound Annual Growth Rate (CAGR) for each iteration

- **Description:** A dictionary with statistics of Compound Annual Growth Rate (CAGR) for each iteration.
- **Variable:** `results_cagr_describe`
- **Usage:** This dictionary calculates and summarizes the annual growth rate of an investment for each simulation iteration.

### Portfolio profits

#### Profits Pandas Series for each iteration

- **Description:** A dictionary with profits Pandas series for each iteration.
- **Variable:** `portfolio_profits`
- **Usage:** This dictionary contains Pandas series representing the profits observed in each iteration, offering a detailed view of the portfolio's financial performance over time.

## Visualizations

Histograms with confidence interval (95% confidence level), boxplots and other visualizations will be generated based on the aforementioned results to provide a clear and insightful representation of the portfolio's performance distribution across iterations.

## Simulation parameters

- `analysis_currency` - Currency in which the simulation is run.
- `start_date` - Start date of simulation data. If start_date is before the first available date of the securities, the first available date will be used.
- `end_date` - End date of simulation data.
- `tickers_and_currencies` - A dictionary where the keys are for securities tickers and the values are for currencies for the corresponding securities.
- `weights` - A dictionary conatining weight groups names as keys and the securities name list (tickers characters before the dot) as the corresponding values.
- `expense` - Amount of expense (transaction fee) for each transaction.
- `amount` - Approximate amount of money to invest in each transaction.
- `ohlc` - Which column to use for open, high, low, close prices.
- `iterations` - Number of iterations for the Monte Carlo simulation.
- `n_months` - A number representing the interval between transactions starting from the month specified in the start_date variable.

## Examples

The code already includes predefined sample parameters.

### Predefined portfolio strategy

Each calendar month we buy specified securities (ETFs) in the corresponding weights for ~1000 euro. Therefore, out analysis currency will be `EUR`.

We will invest in the securities (ETFs) below:

- `VWCE.DE` - Vanguard FTSE All-World UCITS ETF - currency: `EUR`
- `ISAC.L` - iShares MSCI ACWI UCITS ETF USD - currency: `USD`
- `VAGP.L` - Vanguard Global Aggregate Bond UCITS ETF - currency: `GBP`
- `AGGH.MI` - iShares Core Global Aggregate Bond UCITS ETF - currency: `EUR`
- `4GLD.DE` - Xetra-Gold - currency: `EUR`
- `IGLN.L` - iShares Physical Gold ETC - currency: `USD`

The corresponding weights for each of security are:

- `VWCE.DE` - 30%
- `ISAC.L` - 20%
- `VAGP.L` - 10%
- `AGGH.MI` - 20%
- `4GLD.DE` - 10%
- `IGLN.L` - 10%

The date of the first transaction is some day in `2019-08`. Hence, the analysis will be carried out in the period from September 2019 (each iteration one random date from this month) up to November 2023 (depends on the `n_months` variable, in our case it will be equal to 1). We will analyse close prices as they are usually the best for such analysis.

The simulation wil be performed with 1000 iterations.

### Results

#### Plot with the mean profit for each date over all iterations

Lightblue colour around main line indicates error bands made with confidence interval (95%) from all iterations values.

![image](https://github.com/mrkyc/portfolio-simulations/assets/82812493/f2c89666-1400-4616-9df8-4183fa1f7c35)

#### Plot with mean profit for each iteration with confidence interval (95%)

![image](https://github.com/mrkyc/portfolio-simulations/assets/82812493/b1314a25-d7c8-48bd-9465-4e434cbeba6d)

#### Boxplot with the maximum profit for each iteration

![image](https://github.com/mrkyc/portfolio-simulations/assets/82812493/39e83c30-917c-434f-934e-e72522055d0d)

#### Boxplot with the maximum percentage profit for each iteration

![image](https://github.com/mrkyc/portfolio-simulations/assets/82812493/abcd99fe-332d-45ae-bf4d-755f436f3238)

#### Boxplot with the minimum profit for each iteration

![image](https://github.com/mrkyc/portfolio-simulations/assets/82812493/7dba1675-d40e-4f1f-ba1d-1ffe3bf908ff)

#### Boxplot with the minimum percentage profit for each iteration

![image](https://github.com/mrkyc/portfolio-simulations/assets/82812493/ebe1f2ff-9642-4439-94c7-4ce0574e757e)

#### Plot with the mean drawdown for each iteration with confidence interval (95%)

![image](https://github.com/mrkyc/portfolio-simulations/assets/82812493/b37f9382-eb35-4398-8b45-655307950bf9)

#### Boxplot with the lowest drawdowns for each iteration

![image](https://github.com/mrkyc/portfolio-simulations/assets/82812493/75f2c704-328e-4296-9010-5abc7b237d7d)

#### Plot with the mean CAGR (calculated for each transaction made > 365 days ago) for each iteration

![image](https://github.com/mrkyc/portfolio-simulations/assets/82812493/66af686d-76fe-45da-8de6-8b555ffa1d1f)

#### Boxplot with the best transactions CAGR for each iteration

![image](https://github.com/mrkyc/portfolio-simulations/assets/82812493/ba0d113d-c9c8-4517-9733-7865adc9b981)

#### Boxplot of the worst transactions CAGR for each iteration

![image](https://github.com/mrkyc/portfolio-simulations/assets/82812493/d22bc436-2caf-4568-ab5a-96b799a239ec)
