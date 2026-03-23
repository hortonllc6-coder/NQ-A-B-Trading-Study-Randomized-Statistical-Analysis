# Monte Carlo–Informed A/B Study: Stop-Loss & Take-Profit Optimization in Nasdaq-100 Futures

> Prospective randomized controlled trial · 100 live trades · 5,000-iteration bootstrap resampling · Python + R

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![R](https://img.shields.io/badge/R-276DC3?style=flat&logo=r&logoColor=white)
![Status](https://img.shields.io/badge/Status-In%20Progress-yellow)

---

## 01 — What I tested

- **Primary question:** Does a higher reward-to-risk ratio (2:1) produce meaningfully better profitability than a tighter ratio (1.5:1) in short-term NQ futures trading, or does the tighter ratio yield greater daily consistency?
- **Arm A** used TP/SL = $300/$150 (R:R = 2.0) — targeting higher per-trade upside at the cost of wider variance.
- **Arm B** used TP/SL = $150/$100 (R:R = 1.5) — targeting smaller, more frequent wins and a smoother equity curve.
- All trades executed during the 9:30–11:00 AM ET session on Nasdaq-100 futures, capped at 6 trades/day with a $300 daily loss limit and $500 daily profit target.

---

## 02 — How I did it

- **Experimental design:** Prospective randomized A/B trial with randomized block assignment at the trade level. 100 total trades across a 2-week simulated evaluation period (50 per arm).
- **Data collection:** Trade-level log capturing entry/exit times, direction, P&L (USD), R-multiple, MFE/MAE, intraday drawdown, trend regime, and volatility regime.
- **Statistical tests:** Welch's t-test, Mann-Whitney U, Two-proportion z-test, Bootstrap resampling (5,000 iterations), Cohen's d, OLS regression (P&L ~ Arm + Volatility + Trend).
- **Execution friction:** $15/trade friction adjustment applied post-analysis. Monte Carlo simulation used for forward-looking outcome modeling.

---

## 03 — Key findings

| Metric | Arm A (TP $300 / SL $150) | Arm B (TP $150 / SL $100) |
|---|---|---|
| Mean trade P&L | $93 | $70 |
| Win rate | 54% | **68%** |
| Profit factor | 2.35 | **3.19** |
| Daily SD | $384 | **$216** |
| Post-friction mean | $78/trade | $55/trade |

- **No statistically significant difference** in mean per-trade P&L (p > 0.05). Bootstrap 95% CI: [−$50, +$100] — overlapping intervals.
- **Cohen's d ≈ −0.25** (small effect): Arm A's dollar advantage is not practically large when normalized for risk.
- **Practical takeaway:** Arm A favors traders tolerating volatility for larger upside. Arm B favors consistency — higher win rate, smoother equity curve, superior profit factor.
- **Execution friction matters:** $15/trade friction reduced Arm A expectancy 18%. Marginal strategies become unprofitable under real-market costs.

---

## 04 — Tools & stack

```
# Analysis
Python      pandas · scipy · matplotlib · seaborn · numpy
R           bootstrapCI · ggplot2 · lm()

# Statistical methods
Welch t-test · Mann-Whitney U · Two-proportion z-test
Bootstrap resampling (n=5,000) · OLS regression · Cohen's d

# Documentation
Notion      structured research log (Methods → Results → Discussion)
Google Colab  Monte_carlo.ipynb
```

---

## 05 — What's next

- **Expand to 120+ trades** to hit the pre-specified stopping rule threshold and achieve adequate statistical power.
- **Regime-stratified analysis:** Rerun regression controlling for trend and volatility regime to determine whether one arm dominates under specific market conditions.
- **Live market validation:** Transition to a funded Topstep $50K Combine account to test whether results hold under real execution constraints.
- **Adaptive parameter modeling:** Explore dynamic TP/SL sizing based on intraday ATR rather than fixed dollar targets.
- **Methodology transfer:** Apply this A/B framework to content performance testing, HR intervention analysis, and product experiment design — demonstrating generalizability beyond trading.

---

*Author: Sydney Horton · Atlanta, GA · Oct 2025 – Present*  
*Status: In Progress · Full paper forthcoming*  
*Note: The A/B testing methodology used here directly maps to product experiment design, marketing campaign analysis, and people analytics interventions.*
