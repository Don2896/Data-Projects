Bitcoin & Ethereum: Volatility, Correlation, and Diversification Analysis

📌 **Decision Context**

A client/investor is considering exposure to digital assets as part of a broader investment portfolio. Following periods of strong price appreciation in Bitcoin and Ethereum, the client wishes to evaluate whether allocating capital to cryptocurrencies can be done in a risk-aware and diversified manner.

Bitcoin (BTC) and Ethereum (ETH) are the two largest and most established cryptocurrencies by market capitalisation. Before committing capital, the client seeks to understand:

Whether exposure to a single cryptocurrency is sufficient, or

Whether holding both BTC and ETH provides meaningful diversification benefits.

The primary risk under consideration is extreme price volatility and the potential for correlated losses during periods of market stress.

🎯 **Primary Business Question**

Should Bitcoin and Ethereum be treated as distinct risk assets within a diversified portfolio, or do their volatility and correlation characteristics limit diversification benefits?


🔍 **Scope of Analysis**

Assets analysed:

- Bitcoin (BTC)
- Ethereum (ETH)
- Data frequency: Daily closing prices
- Time horizon: Multi-year historical period capturing multiple market regimes

Analytical focus:
- Volatility dynamics
- Correlation and co-movement
- Behaviour during periods of market stress
- Intended use: Portfolio risk and diversification assessment

🚫 **Out of Scope**
This analysis does not:
- Forecast future prices or returns
- Provide trading or investment recommendations
- Identify causal drivers of price movements
- Compare BTC and ETH to other cryptocurrencies or asset classes

📐 **Assumptions**

The following assumptions guide the analysis:
- Risk, volatility, and correlation are measured using returns rather than prices:
  Prices are non-stationary and trend over time. Returns capture relative change and allow meaningful comparison of variability and co-movement.

- Log returns approximate percentage price changes:
  Log returns handle compounding naturally, are additive over time, and exhibit more stable statistical properties.

- Daily data is sufficient to capture risk dynamics:
  Daily frequency balances informational richness with statistical stability.

- Correlation is descriptive, not causal:
  Observed correlations reflect co-movement, not cause-and-effect relationships.

- Market reactions are analysed observationally:
  Markets often anticipate events; price responses are not deterministic.



📊 **Deliverable — Executive Summary**
Objective:

This analysis evaluates whether Bitcoin (BTC) and Ethereum (ETH) provide meaningful diversification benefits when held together in a portfolio. It examines price behaviour, volatility dynamics, and correlation patterns across both normal and high-stress market regimes to inform risk-aware investment decisions.

Data & Methodology:

Daily closing price data for BTC and ETH (GBP-denominated) was sourced from Yahoo Finance. Risk and co-movement were assessed using log returns rather than prices to ensure stationarity and meaningful volatility measurement.

Key analytical techniques included:

- 30-day rolling volatility to capture time-varying risk

- 30-day rolling correlation to assess co-movement

- Stress regime classification based on elevated BTC volatility (top quartile)

Key Findings:

- Ethereum exhibits consistently higher volatility than Bitcoin, indicating greater standalone risk.

- BTC and ETH show persistently high correlation, frequently above 0.8, across most market conditions.

- Correlation increases during high-volatility (stress) regimes, with median correlations approaching ~0.9.

- Periods of reduced correlation are short-lived and quickly revert to elevated levels, suggesting shared underlying risk drivers.

Interpretation:

Although BTC and ETH differ in volatility magnitude, their price movements remain strongly aligned — particularly during market stress. This behaviour limits their effectiveness as independent diversification assets. While Ethereum may amplify returns during bullish periods, it also amplifies downside risk without providing meaningful hedging benefits relative to Bitcoin.

Conclusion:

From a portfolio construction perspective, Bitcoin and Ethereum should be treated as highly correlated risk assets rather than distinct diversifiers. Investors seeking diversification within or beyond crypto markets should prioritise assets with structurally lower correlations, especially during stress periods when diversification is most valuable.
