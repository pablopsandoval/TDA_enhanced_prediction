# Financial Time Series Forecasting with TDA and N-BEATSX

This repository contains an **experimental study on financial time series forecasting** that combines **Topological Data Analysis (TDA)** with **deep learning**, specifically the **N-BEATSX** architecture.

The project investigates whether **topological descriptors derived from persistent homology** can provide incremental predictive value when used as **exogenous variables** in deep learning models for financial time series.

---

## 📌 Project Motivation

Financial time series are notoriously difficult to forecast due to:
- high noise levels,
- non-stationarity,
- regime changes,
- complex temporal dependencies.

Recent research suggests that **Topological Data Analysis (TDA)** can capture global geometric and structural properties of time series that are not easily encoded by traditional indicators.

This project explores the following question:

> **Do TDA-based features improve the predictive performance of deep learning models in financial time series forecasting?**

---

## 🧠 Methodology Overview

### Data
- **Assets:** 10 large-cap U.S. stocks  
  (AAPL, MSFT, GOOGL, AMZN, NVDA, META, TSM, LLY, BRK-B, NVO)
- **Period:** January 2019 – October 2025
- **Frequency:** Business days
- **Target:** Scaled daily log-returns (`MinMax`)

---

### Models
Two panel forecasting models were compared:

1. **Baseline Model**
   - N-BEATSX
   - Standard exogenous variables:
     - calendar effects (day of week, month, end-of-month, etc.)
     - market state variables (VIX, realized volatility)

2. **TDA-Enhanced Model**
   - Same N-BEATSX configuration
   - Adds **TDA-based historical exogenous features**:
     - Persistence diagram amplitude (H1)
     - Number of persistent points (H1)
   - TDA features computed from:
     - Takens delay embedding
     - Vietoris–Rips complexes
     - Sliding windows of 21 business days

Both models share identical architecture, preprocessing, and evaluation settings to ensure a **fair comparison**.

---

## 🧪 Experimental Design

- **Forecast horizon:** 5 business days
- **Evaluation:** Rolling-origin backtesting (4 windows)
- **Metrics:**
  - MAE
  - MAPE
  - RMSE
  - MASE

The focus is on measuring the **marginal contribution of TDA features**, not on hyperparameter optimization.

---

## 📊 Key Results

- Incorporating TDA features led to:
  - ~4.5% reduction in MAPE
  - ~1–2% improvement in MAE and MASE
- RMSE remained largely unchanged.
- In ~64% of forecasted points, the TDA-enhanced model produced lower absolute error.
- Improvements were **moderate but consistent**, and **asset-dependent**.

These results suggest that **topological descriptors capture complementary information**, but do not dramatically change predictive performance.

---

## ⚠️ Pilot Study & Lessons Learned

An initial pilot experiment used a **custom N-BEATS implementation** with aggressive preprocessing (wavelets, strong denoising).  
This approach resulted in:
- near-constant predictions,
- worse performance than naïve baselines,
- excessive information loss.

**Key lesson:**  
> Over-denoising financial time series can remove precisely the variability that carries predictive signal.

This motivated a shift toward:
- simpler target transformations,
- a stable public implementation (`neuralforecast`),
- and a clearer focus on the role of TDA features.

---

## 🧩 Conclusions

- **TDA features provide incremental predictive value**, but not a breakthrough.
- N-BEATSX is **not ideal for trading-oriented objectives**, where directional accuracy matters more than point forecasts.
- The real potential of TDA in finance likely lies in:
  - classification tasks (up/down),
  - regime detection,
  - decision-oriented models.

This project should be viewed as a **methodological exploration**, not a production-ready trading system.

---

## 🚀 Future Work

- Reformulate the problem as **directional classification**
- Combine TDA with technical indicators
- Explore regime-switching or hybrid architectures
- Evaluate economic utility instead of pure forecast error

---

## 🛠️ Tools & Libraries

- Python
- `neuralforecast`
- PyTorch
- Pandas, NumPy
- Topological Data Analysis libraries

---

## 📄 Reference

This repository is based on the experimental report:

*Análisis de series de tiempo financieras implementando métodos de TDA*  
ITESM, Monterrey, 2025 :contentReference[oaicite:0]{index=0}
