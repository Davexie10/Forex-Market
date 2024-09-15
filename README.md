# FX Asset Classification and Long-Short Trading Strategy

## Project Overview

This project focuses on applying machine learning techniques to classify financial assets and construct efficient trading strategies in the FX market. Retail investors often rely on intuition or outdated information when building portfolios, leading to suboptimal results. This project uses data-driven analysis and machine learning to make more informed decisions.

## Purpose

The goal is to classify assets into three categories (forecastable, undefined, and non-forecastable) and use these classifications to construct efficient long-short trading strategies. By leveraging regression analysis, we aim to minimize risk and maximize return for currency pairs over a defined time period.

## Methodology

1. **Asset Classification**:
   - A weighted average base portfolio of liquid assets is created, with assets classified as forecastable, undefined, or non-forecastable based on the Mean Squared Error (MSE) from a regression test.
   - The assets are labeled and trained using a classification model (Naive Bayes), and new datasets are categorized to optimize investment selection.
   
2. **Trading Strategy**:
   - The strategy involves long-short positions, taking long positions on underpriced assets and short positions on overvalued ones. The FX market example features USD/JPY and GBP/USD.
   - Regression analysis and timing factors are used to decide which assets to long or short.
   - A reinvestment strategy with a 1:1 long-short ratio is followed to maintain balance within the investment horizon.

## Key Results

- **Classification**: Various currency pairs were successfully classified, though some results deviated from historical intuition due to small dataset sizes or currency behavior shifts.
- **Trading**: Over a 3-hour horizon, the strategy yielded a 0.1511% return in the first round, with a total return of 0.3639% after reinvestments. When annualized, this demonstrates high potential, though real-world application would factor in fees and frequency limits.

## Future Improvements

1. Use weighted average portfolio prices to compute correlations more accurately.
2. Include more currency pairs to diversify the base portfolio.
3. Rebalance the trading portfolio over time to maintain strategy effectiveness.
4. Enhance entry and exit points by incorporating volatility and FD measurements for better directional predictions.

