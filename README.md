# FIFA World Cup 2026 Prediction Model

A machine learning-based project designed to predict match outcomes for the **FIFA World Cup 2026**. The model analyzes historical match data, team statistics, FIFA rankings, recent performance, and other relevant features to estimate the probability of a **win, draw, or loss**.

**▶ Live predictions (full 48-team, 50,000-simulation model):** **https://cup26matches.com**
· [How it works / methodology](https://cup26matches.com/en/methodology/)
· [Live insight feed](https://cup26matches.com/en/live/)
· [Interactive bracket simulator](https://cup26matches.com/en/simulator/)

## Project Overview

The FIFA World Cup 2026 Prediction Model uses data analysis and machine learning techniques to predict possible match results and tournament outcomes.

The main objectives of this project are to:

* Analyze historical international football data
* Compare team performance and strength
* Predict match outcomes
* Estimate win, draw, and loss probabilities
* Simulate the FIFA World Cup 2026 tournament
* Identify teams with a higher probability of winning the tournament

## Quick start

No dependencies. Node 18+.

```bash
git clone https://github.com/dineshkumar200705-hue/world-cup-2026-prediction-model.git
cd world-cup-2026-prediction-model

node predict.mjs brazil argentina      # head-to-head probabilities
node predict.mjs usa mexico usa        # 3rd arg = home team (host bonus)
node backtest.mjs                      # reproduce the accuracy numbers
node calibrate.mjs                     # rebuild ratings from data/results.json
```

Example:

```
$ node predict.mjs spain germany

  spain (Elo 2074)  vs  germany (Elo 1927)   [neutral]

  spain            win   53.2%  ████████████████
  draw                   26.8%  ████████
  germany          win   20.0%  ██████
```

## How it works

1. **Team strength (Elo).** Each nation starts from a long-run prior, then is calibrated on
   recent real internationals — wins over strong sides in important games move a rating more than
   friendlies, and recent form outweighs old form. See [`calibrate.mjs`](./calibrate.mjs).
2. **Each match (Dixon-Coles Poisson).** Ratings → expected goals → a Dixon-Coles bivariate
   Poisson gives win/draw/loss probabilities. The Dixon-Coles correction fixes plain Poisson's
   well-known under-count of low-scoring draws (0-0, 1-1). See [`elo.mjs`](./elo.mjs).
3. **The tournament (Monte Carlo).** The live site plays all 104 matches **50,000 times** through
   the real bracket to get championship & advancement odds — and, now the tournament is underway,
   **locks every finished result** (real standings, real qualifiers, real bracket slots) and
   simulates only what's left. Full write-up:
   [cup26matches.com/methodology](https://cup26matches.com/en/methodology/).

## Files

| File | What |
|---|---|
| `elo.mjs` | The match model — Elo, Dixon-Coles τ, Poisson, `matchProb`, `sampleMatch` |
| `calibrate.mjs` | Build calibrated ratings from `data/results.json` |
| `backtest.mjs` | Walk-forward out-of-sample evaluation (RPS, log-loss, Brier, ECE + reliability curve) |
| `predict.mjs` | CLI head-to-head predictor |
| `track-record.mjs` | Regenerates the live 2026 track-record table in this README |
| `data/results.json` | 913 real international results (Oct 2023 – Jun 2026) |
| `data/elo-calibrated.json` | Calibrated Elo for the 48 finalists |
| `data/wc2026-results.json` | Finished 2026 World Cup matches (feeds the track record) |
| `data/model-backtest.json` | Saved backtest metrics |

## ⚠️ Disclaimer

This project is created for educational and research purposes only. Predictions are generated using historical data and machine learning techniques. Actual match results may differ because of factors such as player injuries, team strategy, weather conditions, and unexpected events.

## 🤝 Contributing

Contributions are welcome.

To contribute:

1. Fork this repository
2. Create a new branch

```bash
git checkout -b feature/new-feature
```

3. Make your changes
4. Commit your changes

```bash
git commit -m "Add new feature"
```

5. Push the branch

```bash
git push origin feature/new-feature
```

6. Create a Pull Request

## 👨‍💻 Author

**DineshKumar**

GitHub: `https://github.com/dineshkumar200705-hue`

## ⭐ Support

If you find this project useful, consider giving the repository a ⭐.
