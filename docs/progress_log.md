# Research Documentation: Evolution of Volatility Forecasting and AI Agency

## I. Fall Quarter: Exploratory Phase & LLM Domain Adaptation (Weeks 1–10)

The research project was initiated to explore the intersection of **Generative AI and Quantitative Finance**, with a particular focus on the role of **Large Language Models (LLMs)** in market volatility analysis. The goal was to evaluate whether domain-specific LLMs could assist in identifying volatility patterns, early warning signals, and risk factors from multi-market datasets.

---

### Weeks 1–2: Framework Assessment

Conducted a comparative analysis of open-source financial LLMs:

- **FinGPT**
- **FinBERT**

These were compared against proprietary platforms such as:

- **BloombergGPT**
git add research_progress.md

- **Conditional Coverage (CC)**  
  Tests whether VaR violations occur independently or cluster over time.

---

### Regulatory Loss Functions

- **Lopez Quadratic Loss (RQL)**  
  Penalizes the magnitude of VaR violations.

- **Caporin_1 (RC_1)**  
  Measures performance under extreme market conditions with emphasis on tail risk.

---

## Preliminary Findings

The **GARCH–Time-MoE hybrid model** demonstrates:

- Lower rejection rates in UC and CC tests compared to baseline models
- Reduced prediction error during extreme volatility events
- Greater stability in rolling VaR forecasts

These results suggest improved robustness to **market regime shifts** compared to traditional econometric or standalone deep learning models.