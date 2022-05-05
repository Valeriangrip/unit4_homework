# Pandas Unit 4 Assignment - A Whale Off the Port(folio)

## Requirements

The purpose of this assignment is to develop a comprehensive tool for assessing portfolios using quantitative analysis techniques with Python and Pandas.

The main tasks include reading and cleaning data, determining the success of each portfolio, and choosing and evaluating a custom portfolio.

The analysis consists of computing and visualizing various financial metrics, volatility, returns, risk, and Sharpe ratios, for various whale portfolios, algorithms, an index, and a custom portfolio of stocks.

## Approach

The approach for this assignment was to complete the starter code by applying what I learned from classes and the materials. For each section, I looked at the sample code and added it to my assignment when I understood it would satisfy the requirement. For example, trying to answer Risk Analysis "which portfolio is riskier" required me to review the slide deck and sample code from unit 3 class 3. The starter code and class materials were structured in a way that I could complete this assignment in a step-by-step and straight-forward manner.

For the "Rolling Statistics Challenge: Exponentially Weighted Average" I read the linked documentation and tried something.

To complete the custom portfolio section I used the existing three sample price histories, OTEX, SHOP, and L, and added two more of my own, AAPL and MSFT. The date range used was 2018-01-01 to 2019-12-31. I used the original three files because I started using them before I realized they were just samples. It was good practice go to through the analysis techniques again for this new set of data.

## Sample Dataframe

Symbol	Company	Industry	Offer Date	Shares (millions)	Offer Price	1st Day Close	Current Price	Return	T-10Days	T-90Days	T+100Days	SPY 90D Return	100 day Return	100D Y/N
BLTE	Belite Bio, Inc.	5	1	6.0	$6.00	$10.59	$10.59	76.50%	2022-04-19	2022-02-04	2022-08-07	-0.0208812341177367	0.2766761343681165	1
HLVX	HilleVax, Inc.	5	1	11.8	$17.00	$19.09	$19.09	12.29%	2022-04-19	2022-02-04	2022-08-07	-0.0208812341177367	0.0293347020149954	1
OST	Ostin Technology Group Co., Ltd.	6	1	3.4	$4.00	$39.66	$3.70	-7.50%	2022-04-17	2022-02-02	2022-08-05	-0.0397943592088691	-0.9020423599240946	0
TNON	Tenon Medical, Inc.	5	1	3.2	$5.00	$22.50	$21.61	332.20%	2022-04-17	2022-02-02	2022-08-05	-0.0397943592088691	0.49022216796875	1
JCSE	JE Cleantech Holdings Limited	6	1	3.8	$4.00	$19.00	$4.35	8.75%	2022-04-12	2022-01-28	2022-07-31	-0.0015009384241898	-0.6905263097662675	0
APLD	Applied Blockchain, Inc.	9	1	8.0	$5.00	$4.85	$3.36	-32.80%	2022-04-03	2022-01-19	2022-07-22	0.0057046442529117	-0.3525772852273781	0
EE	Excelerate Energy, Inc.	7	1	16.0	$24.00	$26.85	$27.25	13.54%	2022-04-03	2022-01-19	2022-07-22	0.0057046442529117	-0.0225325710853197	0
GNS	Genius Group Limited	3	1	3.3	$6.00	$30.50	$5.75	-4.17%	2022-04-02	2022-01-18	2022-07-21	-0.0047381500647333	-0.7986885289676854	0
XPON	Expion360 Inc.	6	1	2.2	$7.00	$7.93	$3.59	-48.71%	2022-03-22	2022-01-07	2022-07-10	-0.043595506680651	-0.518915493089018	0
ANTX	AN2 Therapeutics, Inc.	5	1	4.6	$15.00	$15.40	$15.63	4.20%	2022-03-15	2021-12-31	2022-07-03	-0.1220313073124193	0.100649427454798	1
AKAN	Akanda Corp.	5	1	4.0	$4.00	$10.50	$8.49	112.25%	2022-03-05	2021-12-21	2022-06-23	-0.0667084342650852	-0.1671428680419922	0



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
