# Pandas Unit 4 Assignment - A Whale Off the Port(folio)

## Requirements

The purpose of this assignment is to develop a comprehensive tool for assessing portfolios using quantitative analysis techniques with Python and Pandas.

The main tasks include reading and cleaning data, determining the success of each portfolio, and choosing and evaluating a custom portfolio.

The analysis consists of computing and visualizing various financial metrics, volatility, returns, risk, and Sharpe ratios, for various whale portfolios, algorithms, an index, and a custom portfolio of stocks.

## Approach

The approach for this assignment was to complete the starter code by applying what I learned from classes and the materials. For each section, I looked at the sample code and added it to my assignment when I understood it would satisfy the requirement. For example, trying to answer Risk Analysis "which portfolio is riskier" required me to review the slide deck and sample code from unit 3 class 3. The starter code and class materials were structured in a way that I could complete this assignment in a step-by-step and straight-forward manner.

For the "Rolling Statistics Challenge: Exponentially Weighted Average" I read the linked documentation and tried something.

To complete the custom portfolio section I used the existing three sample price histories, OTEX, SHOP, and L, and added two more of my own, AAPL and MSFT. The date range used was 2018-01-01 to 2019-12-31. I used the original three files because I started using them before I realized they were just samples. It was good practice go to through the analysis techniques again for this new set of data.

## Code Snippets & Outputs

```
# Use `ewm` to calculate the rolling window
all_data.ewm(halflife='21 days', times=all_data.index).mean()
```

![Rolling Statistics Challenge: Exponentially Weighted Average](/Resources/output3.png)

```
# Calculate the correlation
price_corr = all_data.corr()
# Display de correlation matrix
sns.heatmap(price_corr, vmin=-1, vmax=1)
```

![Rolling Statistics Challenge: Exponentially Weighted Average](/Resources/output4.png)

```
# Calculate and plot Beta
# Calculate covariance of a single portfolio (Custom & S&P TSX)
custom_covariance = all_portfolio_df['CUSTOM'].cov(all_portfolio_df['S&P TSX'])

# Calculate variance of S&P TSX
custom_variance = all_portfolio_df['S&P TSX'].var()

# compute beta
custom_beta = custom_covariance / custom_variance

# Plot beta trend
# Calculate 60-day rolling covariance of CUSTOM PORTFOLIO vs. S&P TSX
custom_rolling_covariance = all_portfolio_df['CUSTOM'].rolling(window=60).cov(all_portfolio_df['S&P TSX'])

# Calculate 60-day rolling variance of S&P TSX
custom_rolling_variance = all_portfolio_df['S&P TSX'].rolling(window=60).var()

# Calculate 60-day rolling beta of CUSTOM PORTFOLIO and plot the data
custom_rolling_beta = custom_rolling_covariance / custom_rolling_variance
custom_rolling_beta.plot(figsize=(20, 10), title='Rolling 60-Day Beta of CUSTOM PORTFOLIO')

# Showcase beta vs. correlation by plotting a scatterplot using the seaborn library and fitting a regression line
sns.lmplot(x='S&P TSX', y='CUSTOM', data=all_portfolio_df, aspect=1.5, fit_reg=True)
```

![Rolling 60-Day Beta of CUSTOM PORTFOLIO](/Resources/output1.png)

```
# Calculate Annualized Sharpe Ratios
all_sharpe_ratios = (all_portfolio_df.mean() * 252) / all_portfolio_annual_std
all_sharpe_ratios

# Visualize the sharpe ratios as a bar plot
all_sharpe_ratios.plot.bar(title="All Sharpe Ratios")
```

![Sharpe ratios](/Resources/output2.png)
