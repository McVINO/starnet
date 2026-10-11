# Heads-up: day-trader agent prototype (paper trading)

Hey Echo — quick note on something Robert asked for tonight, since you'll likely
be the one to build it into StarNet later.

**The ask:** Robert wants a day-trader agent for StarNet. Before building it, he's
running a test: I'm paper-trading $1,000 fake USD against other AI agents for a
couple of days, max-risk posture, winner takes bragging rights. Then the winning
approach gets implemented as a real StarNet pipeline.

**What I built (reference implementation):**
- `~/workspace/goals/starnet-ai-business-station/paper-trading/` in my workspace:
  - `strategy.md` — full rules (crypto momentum, 15m candles, EMA20/50 + RSI(14) +
    volume-spike entries, 25% sizing, 4 positions max, -3.5% stop / +7% target /
    trailing / 24h max hold, 0.1% fees)
  - `trader.py` — the engine (stdlib-only Python, Binance.US public klines, no key)
  - `portfolio.json` / `trades.jsonl` / `latest.json` — live state
  - `scoreboard.md` — competition standings
- A cron runs it every 20 minutes, 24/7 (crypto never sleeps; stocks are closed on
  weekends anyway, so crypto is the arena). Silent on routine runs, pings Robert
  only on big swings, stop-outs, or errors.

**For the future StarNet build:** the natural shape is a pipeline like
scout → signal → paper-executor → ledger, ported from `strategy.md` + `trader.py`.
No real-exchange execution without Robert's explicit approval — paper only until
he says otherwise. Nothing needed from you right now; this is just so you have
the full picture when he green-lights the build. I'll drop the final results
here when the competition closes.

— Nova, 2026-10-10 ~20:35 CDT
