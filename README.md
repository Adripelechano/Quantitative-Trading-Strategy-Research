# Quantitative Trading Strategy Research

## Summary
This project investigates systematic trading strategies based on trend indicators, market structure, and Smart Money Concepts (SMC) through historical backtesting.

Rather than optimizing a single strategy for maximum historical return, the repository focuses on comparing different trading hypotheses, understanding their risk/return characteristics, and identifying parammeters that produce further investigation.

The current experiments cover approximately one month of data for the first notebook and eight months for the second. Therefore the results should be interpreted as exploratory research rather than evidence of persistent future profitability.

## Repository Structure
* **README.md** - Project overview, methodology, results, and research conclusions.
* **01_trend_indicators_backtest.ipynb** - Backtesting of trend-based strategies and indicator configurations.
* **02_market_structure_backtest.ipynb** - Backtesting of liquidity sweeps and SMC-based market-structure strategies.

## Research & backtesting pipeline

The research follows a common experimental workflow:

Market Data → Signal Detection → Strategy Logic → Risk Management → Backtest → Performance Analysis

The main evaluation metrics are:

* Total Return — cumulative strategy performance.
* Win Rate — percentage of profitable trades.
* Profit Factor — gross profits relative to gross losses.
* Maximum Drawdown — largest peak-to-trough decline.
* Sharpe Ratio — risk-adjusted performance.
* Trade Count — provides context for statistical reliability and trading frequency.

The analysis emphasizes the interaction between return, risk, and trading frequency, instead of just evaluating strategies based on total return alone.

### Notebook 01 — Trend indicators

01_trend_indicators_backtest.ipynb investigates systematic strategies based on trend following indicators and technical signals.

The notebook explores how different indicator configurations affect:

* Signal generation
* Entry and exit conditions
* TP/SL parameters
* Risk adjusted returns
* Statistical characteristics

The objective is to determine whether different trend signals exhibit consistent behavior and which variables should be investigated further.

### Notebook 02 — Market structure

02_market_structure_backtest.ipynb investigates strategies based on market structure and Smart Money Concepts.

The notebook contains two main research blocks:

1. Liquidity Sweeps
2. SMC Structures
   
#### 1: Liquidity Sweeps

The first experiment investigates liquidity sweep setups on a 15-minute timeframe.

The strategy produced negative expectancy during the sample, but also relatively low drawdown.
A possible explanation is the sensitivity of lower timeframe sweeps to market noise. Candle wicks may represent short term volatility rather than real liquidity events, resulting in a high number of false signals and a low win rate.

The 0.96 profit factor is close to breakeven, suggesting that relatively small changes in signal filtering could probably affect performance.

Several modifications could be investigated:

* Higher-timeframe bias: restrict sweeps according to H4/D1 market direction.
* Volume confirmation: require increased volume during the sweep.
* Dynamic thresholds: replace fixed swing windows with volatility-adjusted thresholds such as ATR.
* Multi-timeframe confirmation: combine higher-timeframe structure with lower-timeframe execution.

These hypotheses should be evaluated on separate validation periods rather than optimized exclusively on the current sample.

#### 2: Smart Money Concepts

The second experiment evaluates several SMC-based structures:

* Order Block Extremes (OB_EXTREM)
* Decisional Order Blocks (OB_DECISIONAL)
* Fair Value Gaps (FVG)
* Golden Zone (GOLDEN_ZONE_075)

All four configurations produced positive results during the observed sample, although their performance differ:

* OB_DECISIONAL generated the largest return at 20.39%, but also exhibited the largest drawdown (-3.50%) and higher trading frequency.
* GOLDEN_ZONE_075 produced a more moderate 6.05% return, while showing the highest profit factor (1.40) and Sharpe ratio (4.20) together with the lowest maximum drawdown (-0.70%) from all the tested configurations.
* FVG showed a similar risk-adjusted profile, with a 3.53 Sharpe ratio, 1.29 profit factor, and -1.14% maximum drawdown.

An important characteristic across the experiments is the relatively low win rate, ranging from 28.7% to 31.8%. This indicates that profitability is because of the relationship between winning and losing trade sizes rather than by a majority of winning trades.

The large difference in trade counts is important when comparing these configurations. In particular, OB_DECISIONAL generates 2,636 trades, compared with 440–513 trades for several of the other configurations. Consequently, total return should not be interpreted independently of trading frequency, drawdown, transaction costs, and statistical reliability.

The current results are therefore better interpreted as evidence of different characteristics rather than as a definitive ranking of the strategies.

## Key conclusions:

The experiments overall highlight several important considerations for systematic trading research:

1. Market structure signals are highly sensitive to timeframe and market conditions.
2. Low win rates can still produce positive expectancy when the payoff distribution is asymmetric.
3. Risk-adjusted metrics provide additional information beyond cumulative return.
4. Trading frequency strongly affects the interpretation of historical returns.
5. Parameter and timeframe selection can introduce overfitting risk.

The results should therefore be evaluated across longer periods and different market regimes before reaching to conclusions about robustness.

## Backtesting Limitations

The current experiments represent an initial research stage. Several aspects require further development before the results could be considered realistic representations of live trading:
1. Transaction costs
2. Slippage
3. Execution latency
4. Parameter senssitivity analysis
5. Statistical significance
6. Multiple market regimes
7. Portfolio risk allocation

In particular, the current sample is too short to distinguish between a persistent structural effect and a result specific to the observed market conditions.

## Future work
Based on the previous limitations, the future aims should be:
1. Extend the historical sample across multiple market regimes.
2. Introduce realistic transaction costs and slippage.
3. Analyze parameter sensitivity and optimization with machine learning algorythms.
4. Implement market structure filters, based on volatility and market behaviour.
5. Investigate cross instrument correlations.
6. Develope portfolio allocation methods.

The long-term objective is to move from single-strategy backtesting toward robust, portfolio-level quantitative research, while minimizing overfitting and maintaining a clear separation between in-sample hypothesis generation and out-of-sample validation.
