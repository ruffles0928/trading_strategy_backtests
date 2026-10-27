# SPY Monthly EMA Strategy vs. Buy-and-Hold

I use EMAs (9, 15, 65, 200) on the monthly chart. This project tests whether my trading rules beat simply holding SPY.

**Data:** SPY monthly prices, 1993–2026 (Yahoo Finance). Results cover Sep 2009–Sep 2026, because the 200-month EMA needs the first 200 months to warm up.

## Rules

- Trade only in an uptrend: EMA9 > EMA15 > EMA65 > EMA200
- **Buy** when the monthly candle touches EMA15
- **Sell** when a green candle opens far above EMA9 (top 10% of past candles) and RSI > 80
- **Sell** when the month closes below EMA9

Signals are acted on the next month (no look-ahead), with a 0.05% cost per trade.

## Results

<!-- Paste the results table from Step 13 here -->

![Growth of $1](equity_curve.png)
![Metrics comparison](metrics_comparison.png)
![Trades](trades_chart.png)

The strategy trailed buy-and-hold. Most of the gap came from time in cash: after selling, it only buys back at EMA15, so it missed rallies that didn't pull back (2023, 2026). It also lost more than holding in 2022.

## Limitations

- **one period.** 2009–2026 was mostly a bull market, which makes buy-and-hold very hard to beat. Different decades could tell a different story.
- **Small sample.** Monthly charts produce relatively few trades, so a couple of good or bad trades move the numbers a lot.
- **I designed the rules by looking at charts,** and the thresholds (RSI 80, top 10% stretch) were not tested out-of-sample, so some data snooping is likely.
- **Monthly closes hide what happens inside the month.** Real losses before a sell signal could be larger than shown.
- **Cash earns nothing here,** and the Sharpe ratio assumes a 0% risk-free rate, which understates any strategy that spends time in cash.
- **Taxes are ignored.** Frequent selling realizes gains that buy-and-hold would defer, so after tax the gap would likely be wider.

## Next

- Add a second way to buy back in (e.g. close back above EMA9)
- Test on other ETFs (QQQ, IWM)

## Run it

Open `spy_monthly_ema_backtest.ipynb` in Google Colab and click Runtime → Run all.
