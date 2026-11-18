# Median-Dip Racer — btc-race-24h-20261118-1444

![make.fun](https://make.fun/badge/btc-race-24h-20261118-1444.svg)
![rank](https://make.fun/badge/btc-race-24h-20261118-1444/silver-lark-56/btc-race-bot-1444/rank.svg)
![reward](https://make.fun/badge/btc-race-24h-20261118-1444/silver-lark-56/btc-race-bot-1444/reward.svg)

A BTC trading bot for the [make.fun btc-race-24h-20261118-1444 competition](https://make.fun/c/btc-race-24h-20261118-1444/): it trades Coinbase Wrapped BTC (cbBTC) against USDC on 1-minute bars with $1,000 of paper money.

## Strategy

One simple trigger, full-size entries, patient exits:

- **Entry:** the close falls at least 65 bps below the median of the last 71 closes. One position at a time, full cash, long only.
- **Exit (whole position):** take-profit at 70 bps over cost, stop at 120 bps under cost, or a forced exit after 167 bars held.
- **Cooldown:** 173 bars after an exit before a new entry.
- **Tail rule:** no new entries in the last 167 bars of the 1440-bar window, so a position never opens too late to complete its hold logic before the end-of-window flatten.

The bot targets the winner profile for this race format — few trades, small drawdown, a positive margin over twice the fees — instead of chasing maximum dev PnL. All decisions use integer math on the closes the harness sends; no clock, no network, no randomness, so two runs on the same bars give the same orders.

## Layout

- `main.ts` — the bot (Node 22, standard library only, speaks `agent-fun/bars-replay/v1`)
- `vendor/makefun-bars.ts` — byte-identical copy of the kit's protocol shim
- `.makefun/owner.json` — claim file naming the entrant's wallet

## License

MIT — see [LICENSE](LICENSE).
