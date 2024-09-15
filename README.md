# FX Asset Classification and Long-Short Trading Strategy

## Introduction and Purpose

In the vast financial market, retail investors are often overwhelmed by the number of available investment options. Their choices are frequently based on intuition, random guesses, or outdated information. This often results in portfolios that are far below the efficiency frontier, characterized by higher volatility and lower expected returns, which contradicts the high-risk aversion typically exhibited by retail investors.

While thorough due diligence is ideal for value investors focused on long-term investment horizons, it requires substantial financial expertise and is time-consuming. Data-driven analysis, specifically in the realm of machine learning, provides an efficient alternative for addressing emotional and unsophisticated investment decisions. The purpose of this project is to classify assets into appropriate classes and construct efficient trading strategies using machine learning techniques.

## Techniques Implemented and Procedure Analysis

### Asset Classification

In terms of efficiency, classification, as one of the supervised machine learning techniques, can provide time-sensitive categorization of assets based on selected features. Assets are labeled into three categories: forecastable, undefined, and non-forecastable.

#### How is Classification Performed?

1. **Weighted Average Base Portfolio**: 
   A weighted average base portfolio of several liquid assets with distinct features is constructed to represent a simple market portfolio. A regression test is performed on the aggregate features of this base portfolio, and the mean squared errors (MSE) of asset prices are identified. 
   - Larger MSE values indicate less forecast accuracy and are assigned as non-forecastable.
   - Smaller MSE values suggest more accurate forecasting ability.
   - Intermediate MSE values are classified as undefined.

2. **Classification Training**: 
   The model is trained on the features of the base portfolio, and the resulting classification scales down the investment pool. This allows decision-makers to choose suitable candidates from the pool for constructing various trading strategies.

### Trading Strategy Implementation

The trading strategy used is a classical **long-short strategy**, aimed at capturing opportunities by:
- Taking **long positions** on underpriced assets.
- Taking **short positions** on overvalued assets.
- Diversifying risk in line with the goal of constructing an efficient portfolio, which minimizes standard deviation while achieving higher expected returns.

The assets in the long and short positions should ideally have a high negative correlation. For example, in the FX market, USD/JPY and GBP/USD have a historical negative correlation (-0.56 over 5 years). A simple linear regression model is run on each trading pair, using a timing factor to represent embedded momentum characteristics. The currency pairs with higher coefficients are expected to have a larger magnitude of momentum.

Positions are opened with a long-short ratio (L-S) equal to 1, mimicking the initial investment capital, and reinvestment is continued at a defined frequency within the investment horizon.

## Intermediate Results

### Portfolio Regression (Best Model: Linear Regression)

- **MSE for EUR/USD**: `0.0002079` (Undefined)
- **MSE for GBP/CHF**: Nearly `0` (Forecastable)
- **MSE for USD/CAD**: `0.0004121` (Non-forecastable)

### Classification Results (Best Model: Naive Bayes)

- **EUR/CHF**: Forecastable (87.1%), Undefined (12.9%)
- **EUR/CAD**: Non-forecastable (100%)
- **GBP/EUR**: Forecastable (100%)
- **GBP/USD**: Non-forecastable (100%)
- **GBP/CAD**: Non-forecastable (100%)
- **USD/CHF**: Forecastable (100%)
- **USD/JPY**: Undefined (100%)

The classification results show some deviation from historical expectations, such as the 100% undefined result for USD/JPY and 100% non-forecastable result for GBP/USD. This could be due to several factors:
- Lack of diversity in the base portfolio construction, as all currency pairs have low MSE values.
- The regression was performed on a small-scale dataset, which needs to be expanded.
- Currency pairs may have experienced behavioral shifts, requiring further analysis.

### Regression Analysis for Long and Short Positions

- **GBP/USD**: Upward trend within the previous 5 hours.
- **USD/JPY**: Downward trend within the previous 5 hours.

Based on this, I decided to **long GBP/USD** and **short USD/JPY**, assuming momentum would continue.

## Final Trading Results

- **Over a 3-hour investment horizon**:
  - First investment return: 0.1511%
  - Reinvestment 1 return: 0.1076%
  - Reinvestment 2 return: 0.1052%
  - **Total return**: 0.3639%
  - **Arithmetic average return**: 0.1213%

Given capital limitations, reinvesting at such a high frequency is impractical. Thus, a return of 0.1511% over a 3-hour period was used as the performance metric. When converted to a daily return, this yields 1.22%, and when annualized, results in a high return (assuming similar conditions persist).

These results indicate that the methodology used is both feasible and effective.

## Improvements

1. Base portfolio correlation should not simply average out the constituents' correlation with exogenous variables. Instead, use weighted average portfolio prices to compute correlations.
2. Construct the base portfolio with more currency pairs to increase diversification.
3. Rebalance the trading portfolio over time to prevent strategy distortion.
4. Entry and exit points should be determined by FD, volatility, and other factors that can estimate movement direction.

## Database and API Information
| Resource        | Description                          | Link                                                    |
|-----------------|--------------------------------------|---------------------------------------------------------|
| **ArcDB**       | Database used for the project        | [ArcDB Documentation](https://www.arcdb.com)            |
| **Polygon API** | API used to retrieve market data     | [Polygon API Documentation](https://polygon.io/docs)    |
