# Crypto Alpha Research — Short-Horizon Signal on Binance Small-Caps

An honest negative result: a real signal that **doesn't survive transaction costs**.

An LSTM predicts the next 1-minute return of `CRCLBUSDT` from cross-sectional features (incl. BTC). Rolling walk-forward, 10 folds, refit each fold. Buy signal = prediction above the 90th percentile of the model's *validation* predictions — frozen before test, and chosen **without reference to costs**, so the measured edge isn't circular.

## Selection

Grid over lookback × horizon on **2026-06-24 → 06-25**. Signal exists at **horizon 1 only** (corr 0.087–0.112, all lookbacks); horizons 5–40 are noise. Chosen: **lookback 60, horizon 1**.

<img width="1178" height="985" alt="image" src="https://github.com/user-attachments/assets/faab459e-100c-4092-9e59-78f8156eb73b" />

## Results

Walk-forward on **2026-06-26 → 06-27** (disjoint from selection), 10 folds.

| | Selected | Unconditional |
|:--|--:|--:|
| Mean return | **+2.24 bps** | +0.22 bps |
| Std err (t) | 0.92 bps (**t = 2.44**) | — |
| % positive | 60.6% | 51.9% |
| n | 297 trades | 2,879 bars |

Round-trip cost (2 × 7.5 bps taker): **15 bps** → **net −12.76 bps/trade**. Positive in 8/10 folds.

> **Statistically detectable, economically dead.** The edge would need to grow ~6× before any threshold clears costs.

## Notes

- **BTC features help notably** — the small-cap's next-bar move is partly market beta.
- **Not a seed artifact** — stable across weight inits; fold variance ≫ seed variance.
- **Close prices only**, so 15 bps is a *lower bound* on true cost (no spread, no depth).
- Caveats: threshold doesn't transport cleanly across folds (4–55 trades vs ~29 expected); t assumes iid trades; one symbol, two days; features are candle-to-candle returns only.
