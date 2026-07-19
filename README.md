# Options Quest

An interactive course that teaches options trading to absolute beginners — one self-contained HTML file, no build step, no dependencies.

## Run it

Double-click **`index.html`** (or open it in any modern browser). That's it.

## What's inside

- **Course** — 29 story-driven lessons across 6 chapters, guided by a mentor named Vega, taking you from "what is a call?" to professional-grade decision making:
  - **Ch. 1 · The Basics (SBUX):** calls, strikes, premium & break-even, puts, expiry, intrinsic vs extrinsic value, selling options.
  - **Ch. 2 · The Greeks (PLTR):** delta, theta decay, implied volatility (including a scripted earnings IV-crush), reading an option chain.
  - **Ch. 3 · Strategies (DIS):** covered calls, cash-secured puts, debit & credit vertical spreads, and a 5-round Gauntlet.
  - **Ch. 4 · Volatility:** the volatility risk premium (implied vs realized — Natenberg), IV rank as the sell/buy signal, straddles & strangles, and the iron condor.
  - **Ch. 5 · The Edge:** expected value over win rate ("resulting"), position sizing & risk of ruin (Ralph Vince's drawdown math), managing winners at ~50% of max / exiting by ~21 DTE (tastytrade mechanics), liquidity, slippage, and tilt discipline.
  - **Ch. 6 · Mastery:** portfolio Greeks & delta-neutral books, post-1987 put skew and the crash premium, Taleb's barbell & tail-risk convexity, the wheel, and a 6-round final exam.
- Each lesson: interactive exercise (simulators for the vol premium, EV, risk-of-ruin, crash/barbell, skew, plus strategy builders) → quick quiz (XP + streak bonuses) → a simulated trade you advance day-by-day → debrief.
- **Practice desk** — a persistent $10,000 simulator that unlocks in 4 tiers after chapter bosses (buy-only → Greeks/selling/expiries → spreads + all tickers → one-tap strategy templates: straddle, strangle, iron condor, credit spreads). PLTR has surprise earnings with IV crush. Naked calls are blocked; short puts must be cash-secured; defined-risk trades hold collateral equal to max loss.
- **Progression** — XP, a rank ladder (Intern → Partner), 1–3 stars per lesson, daily streak.
- **Glossary** — a searchable dictionary of 71 finance terms used in the course (from *strike price* to *gamma scalping* and *barbell strategy*), grouped by topic. Opens as a right-hand drawer from the floating book button on any screen; Esc or the backdrop closes it.

## Philosophies baked into the curriculum

The advanced chapters are grounded in established practitioner research and philosophy:
- **The volatility risk premium** — implied vol persistently exceeds realized vol; options are insurance, priced above fair (Natenberg, *Option Volatility and Pricing*).
- **IV rank mechanics** — sell premium when IV is rich relative to its own 52-week history, buy when cheap; defined risk; ~45 DTE entries, manage winners at ~50% of max, exit by ~21 DTE (tastytrade research).
- **Expected value & "resulting"** — grade decisions, not outcomes; the law of large numbers needs many small trades (Annie Duke's *Thinking in Bets*).
- **Risk of ruin** — position size, not win rate, decides survival; drawdown asymmetry (−50% needs +100%) (Ralph Vince, *The Mathematics of Money Management*).
- **Skew** — the permanent post-1987 crash premium in downside puts, and how income strategies harvest it.
- **Tail risk & the barbell** — convexity, "picking up pennies in front of a steamroller," never selling naked tails, budgeted far-OTM protection (Nassim Taleb, *The Black Swan* / *Antifragile*).
- **The wheel** — CSP → assignment → covered call, with the golden rule: only on stocks you'd genuinely own.
- **Responsive** — single-column reading layout on phones; at ≥960px, trade screens, the course map, and the practice desk switch to two-column desktop layouts.

## How it works (for the curious)

- Options are priced with **Black-Scholes** (Abramowitz–Stegun normal CDF, ~1e-7 accuracy). Delta is analytic; theta/vega are finite-difference so the "per day" theta matches exactly what pressing *Advance 1 day* does.
- Course price paths are **authored day-by-day moves** so every lesson's teaching outcome is guaranteed (e.g. lesson 1.3 always ends above the strike but below break-even). The practice desk uses seeded **geometric Brownian motion** via `mulberry32` + Box–Muller.
- A ±2% bid/ask spread is applied to every quote, so round-tripping costs a little — teaching spread cost for free.
- Progress is saved in `localStorage` under the key **`optionsQuest_v2`** (schema-versioned; corrupt saves fall back to a fresh start). "Erase all progress" lives in Settings.

### Authoring new scenarios

Lessons live in the `LEVELS` array (section 7b of `index.html`) as pure data. A trade scenario is:

```js
{ ticker:'SBUX', S0:100, iv:0.18, dte:10,
  path:[1.2, 0.9, -0.4],          // authored daily % moves
  ivPath:[0.40, 0.40],            // optional per-day IV overrides (IV crush etc.)
  choices:[{label, sub, legs:[{type:'call', side:1, strike:100, qty:1}]}],
  allowSell:true, brief:'…' }
```

Multiple `choices` automatically produce a "how every choice did" leaderboard at resolution.

## Disclaimer

Educational simulation. It uses real ticker symbols (SBUX, PLTR, DIS) for familiarity, but **all prices are simulated** — this is not live market data, and none of the scenarios describe real events. Nothing in it is financial advice.
