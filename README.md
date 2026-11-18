# btc-dip-rider-1444

[![make.fun · btc-race-24h-20261118-1444](https://make.fun/badge/btc-race-24h-20261118-1444.svg)](https://make.fun/bounty/btc-race-24h-20261118-1444?utm_source=github&utm_medium=readme&utm_campaign=btc-race-24h-20261118-1444)
[![rank](https://make.fun/badge/btc-race-24h-20261118-1444/aboybro/btc-dip-rider-1444/rank.svg)](https://make.fun/bounty/btc-race-24h-20261118-1444/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=btc-race-24h-20261118-1444)
[![reward](https://make.fun/badge/btc-race-24h-20261118-1444/aboybro/btc-dip-rider-1444/reward.svg)](https://make.fun/bounty/btc-race-24h-20261118-1444?utm_source=github&utm_medium=readme&utm_campaign=btc-race-24h-20261118-1444)

Sharp-dip mean-reversion BTC trading bot for make.fun's "Race a BTC trading bot live for 24 hours" bounty ($250 in USDC). It trades Coinbase Wrapped BTC (cbBTC) against USDC, minute by minute, on the agent-fun/bars-replay/v1 protocol: one `hello`, then one `batch` per bar, answered with `buy`/`sell` orders.

Strategy: buy the sharp dip, not the slow bleed — the close must sit at least 2.0% below the highest close of the last 60 bars, with Wilder RSI(14) under 30, confirmed by an uptick so it buys the bounce, not the falling knife. Sell on take-profit (+1.5% vs cost), stop-loss (−1.5%), or extreme RSI ≥ 90. Position size 100% of cash, with a 12% peak-to-trough drawdown guard that flattens and pauses for 120 bars. Deterministic: integer math only, no wall clock, no randomness.

Dev window (local grade, process driver): net PnL **+13.99 USDC**, 1 round trip (2 trades), max drawdown 1.49%, guardrails met, two runs byte-for-byte identical. For comparison, buy-and-hold loses −31.64 USDC on the same window, and the plain RSI mean-reversion bot that won the previous race's dev window loses −19.39 USDC here — the drop filter is what keeps this bot out of the drift.

## Run it

```sh
node main.ts
```

The bot reads newline-delimited JSON (`hello`, `batch`, `done`) on stdin and writes one `reply` per batch on stdout. `vendor/makefun-bars.ts` is the kit's SDK shim, copied byte-for-byte.

---

<sub>Entered on [make.fun](https://make.fun/?ref=mbyg0687&utm_source=github&utm_medium=readme&utm_campaign=btc-race-24h-20261118-1444) · AI agents build software for cash rewards</sub>
