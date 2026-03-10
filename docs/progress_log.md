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

#### Key Research Questions

- Can **Low-Rank Adaptation (LoRA)** fine-tuning achieve high-fidelity financial signal extraction without full model retraining?
- Does **Retrieval-Augmented Generation (RAG)** improve contextual understanding of historical market events while reducing inference overhead?

#### Methods

Constructed benchmark queries on market data, including:

- Volatility clustering
- Market regime shifts

Outputs were compared across models for:

- Signal relevance
- Consistency
- Computational efficiency

#### Insight

LoRA enables targeted adaptation of large models with **minimal additional parameters**, making it feasible for our computational environment.

---

### Weeks 3–5: Technical Integration & Strategy Shift

Explored several quantitative finance foundations:

- Multi-market correlation matrices
- Cross-asset interactions
- Option pricing theory (Black–Scholes, binomial trees)

#### Key Discovery

LLM agents could quantify **“market surprise”**, defined as the deviation between **expected and observed market returns**.

#### Strategic Shift

This insight motivated a shift from generic generative tasks toward **volatility-centric modeling**, where market surprise signals could serve as inputs to predictive risk models.

---

### Weeks 6–10: Infrastructure Development

Developed automated pipelines for financial data ingestion and preprocessing.

#### Data Pipeline

- Scraped market time-series and derivatives data using the **Alpha Vantage API**
- Implemented **Jina AI** for document retrieval and knowledge embedding

#### Data Preprocessing

Standardized preprocessing steps included:

- Missing data imputation
- Log-return transformation
- Normalization

#### Outcome

By the end of Fall Quarter, a robust infrastructure was developed for integrating **real-time market signals into AI models**.

#### Decision

The research direction shifted from purely generative LLM outputs toward **structured risk-assessment models**, establishing the foundation for **hybrid econometric–AI approaches**.

---

# II. Winter Quarter: Specialization in Crude Oil Volatility (Weeks 1–5)

Winter Quarter narrowed the focus to **WTI Crude Oil**, chosen for its:

- High volatility
- Pronounced stylized statistical properties
- Importance to global financial stability

---

### Winter Break & Week 1: Crisis Period Identification

Selected testing windows:

- **2007–2009 Global Financial Crisis**
- **2020–2021 COVID-19 Recession**

#### Justification

These periods exhibit extreme volatility characteristics:

- Volatility clustering
- Leptokurtosis (fat-tailed distributions)
- Leverage effects

These properties make them ideal environments for evaluating hybrid volatility models.

---

### Weeks 2–4: Econometric Baseline & GARCH Variants

Converted raw **WTI crude oil prices** into **stationary log-returns** to satisfy the assumptions of GARCH-type models.

#### Evaluated GARCH Specifications

- **sGARCH (symmetric)**  
  Models volatility with equal response to positive and negative shocks.

- **eGARCH / tGARCH (asymmetric)**  
  Captures the **leverage effect**, where negative shocks increase future volatility more than positive shocks.

#### Calibration

Each model was estimated using **Maximum Likelihood Estimation (MLE)**.

#### Observations

- Asymmetric GARCH variants performed better during crisis periods.
- Standard GARCH struggled to capture **extreme tail behavior** in the 2020–21 COVID recession dataset.

---

### Week 5: Hybridization Methodology

Transitioned toward a **hybrid ensemble framework**.

#### Core Idea

GARCH forecasts are transformed into **feature inputs for neural networks**, allowing the model to capture:

- Linear persistence (via GARCH)
- Nonlinear dependencies (via neural networks)

#### Feature Engineering

Features derived from GARCH outputs included:

- Rolling conditional variance
- Standardized residuals
- Shock terms

#### Target Variable

- One-day-ahead **volatility**
- **Value-at-Risk (VaR)** at:
  - 95% confidence level
  - 99% confidence level

#### Preliminary Result

Neural networks were able to exploit **residual structures left unexplained by GARCH models**, improving predictive performance during high-volatility periods.

---

# III. Current Framework: GARCH–Time-MoE & AI Agency (Weeks 6–Present)

The current research direction integrates **econometric volatility models** with **Mixture-of-Experts (MoE) neural architectures**, enabling adaptive weighting across different volatility regimes.

Primary focus remains on **Goal 1**, while **Goal 2** (autonomous trading agent) is planned but not actively pursued this quarter.

---

## Goal 1: GARCH–Time-MoE Hybrid Model

### Time-MoE Architecture

The Time-MoE network dynamically assigns weights to specialized **expert networks** depending on volatility regimes:

- High volatility
- Medium volatility
- Low volatility

Each expert consists of **LSTM layers** trained on residuals from different GARCH variants.

This design enables the model to capture complex **nonlinear volatility structures** beyond traditional econometric models.

---

### GARCH–NN Equivalence

GARCH(1,1) can be reinterpreted as a **specialized recurrent neural network kernel**:

- Recursive variance updates are encoded directly into the network architecture.
- Volatility signals influence predictions throughout the network rather than acting solely as post-hoc features.

---

### Progressive Residual Modeling

The model follows a hierarchical structure:

1. **Linear Modeling**  
   Captures autocorrelation structures in returns.

2. **Time-MoE / LSTM Expert Layer**  
   Models nonlinear dependencies across volatility regimes.

3. **GARCH Layer**  
   Fits remaining residual volatility clusters, improving tail-risk estimation.

---

### Training Strategy

The training objective combines:

- **Mean Squared Error (MSE)** for volatility prediction
- **VaR coverage penalties** to improve tail-risk forecasting

#### Additional Training Details

- Sliding-window training across crisis periods
- Dynamic expert weighting via a **softmax gating network**
- The gating network learns which expert is most relevant at each time step

---

### Observations to Date

Preliminary results indicate that the hybrid model:

- Outperforms single **GARCH** and **LSTM** baselines during extreme volatility
- Benefits from asymmetric GARCH residuals in expert specialization
- Adjusts expert influence dynamically across **pre-crisis, crisis, and post-crisis regimes**

---

## Goal 2: Autonomous AI Agent (Planned)

Conceptual extension of the model:

- Use **one-day-ahead VaR predictions** to dynamically adjust trading positions.

The agent will later be evaluated using **Firm Loss Functions**, which penalize:

- Underestimation of risk (excess exposure)
- Overestimation of risk (lost capital opportunity)

This goal is currently **deferred** to prioritize full validation of the hybrid forecasting framework.

---

# IV. Evaluation & Validation

## Statistical Framework

### Coverage Tests

- **Unconditional Coverage (UC)**  
  Verifies whether VaR violation frequency matches the theoretical confidence level.

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