# The Feasibility Stress Test — Combined Heat & Power Plant (Case Study #6)

Part of [The Feasibility Stress Test](https://github.com/ekalecturer) — real Monte Carlo and financial-engineering case studies for capex decisions.

## The case

A new plant for combined production of electrical and thermal energy (a cogeneration/CHP plant, fueled mostly by natural gas) went through a deterministic cash flow first: NPV of €598.5M, IRR of 35%, payback in 3 years. A full Monte Carlo simulation on the same project, 50,000 trials across four real input distributions with a positive revenue/cost correlation, gave a mean NPV of only €172.9M — a 71% drop from the deterministic figure, the largest optimism gap of any case in this series. The project still cleared its acceptance thresholds most of the time: an 86.1% probability of a positive NPV and a 91.1% probability the IRR beat the 9% discount rate.

## Source

Marić, B., Grozdić, V. (2016). Monte Carlo Simulation in Valuation of Investment Projects. *Proceedings of the 27th DAAAM International Symposium*, pp.0686-0692, B. Katalinic (Ed.), DAAAM International, Vienna. ISBN 978-3-902734-08-2. DOI: 10.2507/27th.daaam.proceedings.099

The full six-page paper was read directly (via a scispace-hosted PDF mirror), not just the abstract. Every confirmed number in this repo is transcribed from the paper's own tables and text. The paper does not name the plant's country; the authors are affiliated with the University of Novi Sad, Serbia, but this repo does not claim a location the paper itself doesn't state.

## Confirmed findings

| Metric | Value |
|---|---|
| Deterministic NPV | €598.5M |
| Deterministic IRR | 35% |
| Monte Carlo mean NPV (50,000 trials) | €172.9M |
| Monte Carlo standard deviation (NPV) | €160.2M |
| Coefficient of variation (NPV) | 0.9266 |
| P(NPV > 0) | 86.1% |
| P(IRR > 9% discount rate) | 91.1% |

## What's in this repo

- `notebook.ipynb` — Python reconstruction of a four-variable Monte Carlo model (triangular revenue, normal gas-dominated cost, uniform investment, triangular discount rate) with a Gaussian-copula correlation between revenue and cost, executed end to end for 50,000 trials.
- `data/confirmed_facts.csv` — every real number transcribed from the paper.
- `data/input_distributions.csv` — the paper's four named input distributions.
- `data/sensitivity_analysis.csv` — the paper's Table 1, the eleven-variable ±10% sensitivity screen.
- `data/notebook_reconstruction_output.json` — this reconstruction's own simulated output, for direct comparison against the paper's real figures.
- `docs/index.html` — an interactive browser-based simulator: adjust the four inputs, click Run, see your own NPV distribution.
- `docs/notebook.html` — a rendered HTML export of the notebook.

## Honesty disclosure

The paper does not publish its underlying cash flow schedule, the exact triangular/normal parameters used inside Crystal Ball, or its exact correlation method between revenue and variable cost. This reconstruction calibrates a simplified 20-year flat-annuity cash flow (after a 4-year construction phase) so the deterministic case reproduces the paper's real €598.5M NPV exactly, then tunes the four distribution spreads so the simulation's coefficient of variation lands almost exactly on the paper's reported 0.9266, and its probability of a positive NPV lands within a few points of 86.1%. That tuning is a deliberate parameter search, not an incidental result, and it is disclosed as such: the reconstruction's absolute mean NPV does not match the paper's €172.9M to the euro, and the notebook says so explicitly rather than overclaiming precision. The paper's own text also contains a minor internal inconsistency (91.1% vs. 91.9% for the IRR success probability), which is flagged rather than silently resolved.

## Run it yourself

```bash
pip install -r requirements.txt
jupyter notebook notebook.ipynb
```

Or open `docs/index.html` directly in any browser — the simulator runs entirely client-side in JavaScript, no server or install required.

## License

MIT. See `LICENSE`.

---

Part of **The Feasibility Stress Test** — real Monte Carlo and financial-engineering case studies for capex decisions.
