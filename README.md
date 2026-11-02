# QuantLab

**Quantitative portfolio research and optimization in Python.**

> **Status: work in progress.** The project is in its early phase (scoping and setup). Nothing below should be read as already implemented unless it is ticked in the roadmap.

## Research question

> Does mean-variance (Markowitz) portfolio optimization deliver a better risk-adjusted performance than an equal-weight allocation, **out of sample**?

Sub-questions:

- How do covariances drive diversification?
- What is the gap between the *estimated* optimum and the *realised* performance?
- When does optimization fail against a simple benchmark?
- How do rebalancing frequency and transaction costs affect the results?

Failures, fragile results and mixed conclusions are valid outcomes. The goal is a reproducible study, not to prove that Markowitz wins.

## Scope

The project is built in three stages. The core mathematical engine comes first and is kept independent of any interface.

### MVP: a verifiable mathematical engine

- [ ] Python environment, Git and tests set up
- [ ] Universe of five EUR-listed equities and study period fixed, data checked
- [ ] Adjusted prices and daily simple returns
- [ ] Mean, volatility, covariance, correlation (explicit annualisation conventions)
- [ ] Portfolio return and variance for given weights
- [ ] Equal-weight and long-only minimum-variance portfolios
- [ ] Two-asset example verified by hand and with `pytest`
- [ ] Plots: normalised prices, correlation heatmap, allocations

### V1: research platform

- [ ] Efficient frontier and Sharpe ratio analysis
- [ ] Chronological out-of-sample backtest with rebalancing and transaction costs
- [ ] Strategy comparison, risk analysis and drawdowns
- [ ] Streamlit and Plotly dashboard
- [ ] Research report and published results

### V2: extensions (only after the core is validated)

- [ ] EUR/USD conversion and currency risk
- [ ] Monte Carlo simulation and advanced risk models

## Mathematical framework

For $n$ assets with weights $w$, expected returns $\mu$ and covariance matrix $\Sigma$:

$$\mu_p = w^\top \mu, \qquad \sigma_p^2 = w^\top \Sigma w$$

Long-only minimum-variance portfolio:

$$\min_w \; w^\top \Sigma w \quad \text{subject to} \quad \mathbf{1}^\top w = 1, \; w_i \ge 0$$

Without the sign constraint, and if $\Sigma$ is invertible, the solution has a closed form:

$$w^* = \frac{\Sigma^{-1}\mathbf{1}}{\mathbf{1}^\top \Sigma^{-1}\mathbf{1}}$$

Formulas are derived by hand first, then implemented and checked against independent calculations.

## Data and conventions (planned)

- **Universe:** five large EUR-listed equities across different sectors, fixed before any experiment.
- **Period:** candidate window 2016-01-01 to 2025-12-31, to be confirmed and documented.
- **Returns:** daily simple returns from adjusted prices.
- **Annualisation:** mean × 252, volatility × √252, covariance × 252, with explicit assumptions.
- **Source:** `yfinance` for exploration, with a dated snapshot kept for reproducibility.

## Methodology principles

- Estimate $\mu$ and $\Sigma$ using only information available before each decision (no look-ahead bias).
- Compare all strategies on the same dates.
- Include transaction costs and state how returns are computed.
- Document the limits of the study, in particular survivorship bias from choosing equities that are still listed today.

## Roadmap

| Phase | Goal | Validation |
|---|---|---|
| 0. Scoping | MVP, assumptions, notes | Decisions written down |
| 1. Setup | Git, Python, environment, `pytest` | Reproducible installation |
| 2. Data | Five EUR equities, cleaned series | Dates aligned, prices checked |
| 3. Statistics | Returns, volatility, covariance, correlation | Hand calculations and tests pass |
| 4. Portfolios | $w^\top\mu$, $w^\top\Sigma w$, equal weight | Two-asset comparison |
| 5. Optimization | Constrained minimum variance | Converged solver, valid weights |
| 6. Frontier | Efficient frontier and ratios | Documented assumptions |
| 7. Backtest | Out-of-sample evaluation | Reproducible, no look-ahead |
| 8. Application | Streamlit and Plotly interface | Working demo |
| 9. Publication | Tests, README, report | Usable and defensible results |

## Repository structure

```text
quantlab/
├── src/quantlab/   # scientific code (independent of any interface)
├── tests/          # pytest tests
├── notebooks/      # exploration
├── data/           # datasets (raw data is git-ignored)
├── docs/           # decisions and project status
└── README.md
```

## Installation

Setup instructions will be added with the first working release.

## Disclaimer

This is an academic and educational project. It does not provide investment advice and makes no claim about future returns.

## Author

Ryad Belkheire, undergraduate student in MIASHS (mathematics, computer science and economics), Université Paris 1 Panthéon-Sorbonne.

## À chaque session (pour moi)

git add .
git commit -m "Implement daily returns calculation"
git pushexit

## Pour revenir dans l'environnemnt virtuel

source .venv/bin/activateil,