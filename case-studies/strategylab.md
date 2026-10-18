# StrategyLab: testing gold trading strategies against overfitting

> A research platform I directed AI coding agents to build for gold (XAUUSD): backtests with real execution costs (bid/ask, spread, slippage, swap) and statistical checks against overfitting. Every test goes into a tamper-evident ledger so multiple-testing correction counts all attempts. Its first study tested three classic strategies and rejected all three. Private project; case study only.

**The problem.** A good-looking backtest is usually overfit: try enough combinations and some will win by chance. Most personal tools do not count how many tests were run, so they cannot correct for it. And a backtest that ignores bid/ask execution, spread and swap overstates results.

**My role.** I defined the goal, the literature to follow, the stack, the data source, the cost calibration against my broker's symbol specification, and the product decisions. AI coding agents (Claude Code, several models split by difficulty) wrote the code under my direction. Every major change was reviewed by an independent audit step. I verify the results and I am accountable for them.

**What it does.**
- **Data:** free Dukascopy M1 bid/ask data in Parquet, a trading calendar with a 5 pm New York cutoff, and a sealed final period (holdout) that no test is allowed to read.
- **Backtest engine:** buys at the ask and sells at the bid; spread, volatility-scaled slippage, overnight swap with triple Wednesday, stop and limit orders, partial closes, latency and daily loss limits. Checked against a pure-Python reference engine.
- **Statistical validation:** Deflated Sharpe Ratio, PBO (CSCV), White Reality Check/SPA, Holm and BHY multiple-testing corrections, walk-forward, random-entry null models, and a promotion gate with explicit rules.
- **Ledger:** every backtest is written to an append-only, hash-chained ledger, so failed attempts cannot be deleted.
- **Interface:** FastAPI backend and a React UI with candlestick charts.

**The first study.** Three classic strategies on XAUUSD, 2006–2024: an exponential moving-average crossover (H1), a Donchian breakout (H4) and an RSI reversal (H1). The search tested 75 configurations; with earlier ledger entries, the correction counts 187 distinct configurations.

| Strategy | Annual Sharpe, full sample | Annual Sharpe, walk-forward out of sample | Verdict |
|---|---|---|---|
| EMA crossover (H1) | 0.22 | 0.02 | Rejected |
| Donchian breakout (H4) | 0.46 | 0.21 | Rejected |
| RSI reversal (H1) | -0.71 | -1.03 | Rejected |

After multiple-testing correction, **none** of the 187 configurations was significant. The sealed holdout was never opened. A "no" is a useful result.

**Scale.** Built in about three days.

| Item | Value (2026-10-18) |
|---|---|
| Registered indicators | 685 |
| Strategy templates | 279 |
| Automated tests | 8,764 collected |
| Backend (Python) | about 42,000 lines, plus about 24,600 lines of tests |
| Frontend (React + TypeScript) | about 11,700 lines |
| Independent audit reports | 8 |
| Ledger entries | 2,438 |

**Stated limitations.**
- The first study used default costs, not a specific broker's. A no-edge result with those costs does not prove there is no edge with others.
- A rejection shows that, **with these rules, this window and these costs**, there is not enough evidence. It does not prove "there is nothing".
- No strategy has passed the gate and the holdout, so there are no live trades from it.
- Personal research project, private repository. Not investment advice.

**What a client can hire from this.** The same method applied to a client's strategy: a report with real costs, out-of-sample testing and an overfitting check, in Python or R, with the answer whatever it is.

---

Private project. The repository is not public; this page is the case study. This is not investment advice, and backtest results do not predict live results.

[Back to profile](../README.md)
