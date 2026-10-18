# XauDesk: a multi-strategy Expert Advisor for gold (MetaTrader 5)

> An MT5 Expert Advisor in MQL5 that runs several XAUUSD strategies at once, with account-protection rules, risk sizing independent of account size, an own volatility indicator and an on-chart panel, plus a Python harness that drives the MT5 Strategy Tester for walk-forward testing. Built with AI agents under my direction, with an independent audit of every research round. Forward test in demo is in progress; no performance claims. Private project; case study only.

**The problem.** Running several strategies in one Expert Advisor is easy to get wrong: risks add up, small accounts cannot size trades properly, and every "improvement" looks good in some period. I wanted one EA that stays controlled and a process that tells a real improvement from noise.

**My role.** I set the goal, the rules for adopting changes, and the product decisions. AI coding agents (Claude Code) wrote the code and the research prototypes under my direction, with work split across models by difficulty: lighter models for documentation and web research, a stronger one for implementation, and a separate one that audited every round. I review the results and I am accountable for them.

**What it contains.**
- **MQL5 EA (about 6,600 lines, 34 files):** modular design with a strategy contract and registry; seven active strategies from different families (price-action, breakout and mean-reversion styles); position sizing that stays consistent across account sizes by carrying forward what the minimum lot cannot trade; an account-protection module (daily loss limit and a pause after a drawdown from peak equity); an order gate that holds orders while the market is closed and retries failed actions; an own volatility-forecast indicator used to scale position size; a trade journal; an on-chart panel; an optional prop-firm mode.
- **Python harness (about 2,500 lines, 21 tests):** drives the MT5 Strategy Tester headless; runs walk-forward (optimize on a training window, validate on the next month); publishes new parameters only if the challenger beats the current champion; analyzes whether a strategy's return is real edge or just market exposure; builds pre-registered drift bands and a block-bootstrap Monte Carlo for the forward test.
- **Parity checks:** the MQL5 indicator and strategies were checked against their Python prototypes.

**How I decided what to keep.**
- Design on data up to 2024; the 2025–26 period is looked at once per hypothesis.
- Acceptance criteria fixed before running a test.
- A change is adopted only if it does not lower the monthly result across several start dates, and the paired direct effect is measured, because small changes in one strategy cascade through the rest of the system.
- An independent AI audit reviewed every research round and could propose tests that change any rule.

**What the process found.**
- Most things were rejected. Six early strategies were removed, 13 candidate families showed no edge after costs, and a trend filter, trade-management rules and active trade correction were all built and left off because none held up.
- Ideas from about ten public gold EA repositories and from a popular trading channel were tested and discarded. In the repository review, one project shipped binaries with remote licensing, so nothing was copied.
- The online learning layer turned out to be leverage, not selection: its weights were not correlated with outcomes. I documented it that way instead of selling it as "AI".
- Re-optimizing a strategy every month did not beat fixed parameters.

**Status and limits.**
- Backtests cover a volatile period for gold; results in earlier years were weaker. I do not publish performance figures.
- A forward test on a demo account started in October 2026. It has too few trades to conclude anything; I compare it against pre-registered bands.
- The EA is not for sale, is not a signal service, and is not investment advice.

**Stack.** MQL5, Python (pandas, NumPy; MetaTrader 5 Python API, read-only), MT5 Strategy Tester, git (94 commits, 16 merged pull requests, about six days), Claude Code.

**What a client can hire from this.**
- Backtest and cost-realism reports for your EA or strategy, with out-of-sample testing.
- Automating the MT5 Strategy Tester and walk-forward runs from Python.
- MQL5 modules: risk sizing, account protection, order handling, on-chart panels.
- A review of how you test and adopt changes, so improvements are not noise.

---

Private project. The repository is not public; this page is the case study. I do not publish performance figures. This is not investment advice, and backtest results do not predict live results.

[Back to profile](../README.md)
