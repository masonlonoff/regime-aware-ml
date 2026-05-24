# Regime-Aware ML for WTI Direction Forecasting

This repository contains a set of final notebooks and supporting files for a regime-aware machine learning project focused on forecasting the next-day direction of West Texas Intermediate (WTI) crude oil prices.

The project combines market regimes, exogenous macro and positioning data, and multiple supervised model families to build and compare direction forecasting strategies. It emphasizes:

- regime-feature construction using a Hidden Markov Model (HMM)
- exogenous feature engineering from CFTC/COT trader positioning and macro data
- multiple supervised models, including Gradient Boosting, ELM, GRU, and FAVAR
- regime-specific modeling and a shared trading strategy for robustness

## Repository Structure

- `notebooks/`
  - `HMM_regimes.ipynb` — build HMM regime features from market and macro data
  - `CFTC_WTI_2.ipynb` — download, preprocess, and engineer CFTC/COT WTI futures features
  - `gradient_boosting_final_paper.ipynb` — gradient boosting models and regime-aware forecasting experiments
  - `ELM_final_paper.ipynb` — extreme learning machine models and comparisons
  - `gru_final_paper.ipynb` — GRU sequence models for price-direction forecasting
  - `favar_final_paper.ipynb` — factor-augmented VAR modeling with regime-aware features
  - `trading_strategy.ipynb` — tuning a common trading strategy across model families

- `VIP_2_Final_Paper.pdf` — final project report

## Project Overview

### Goal

Predict the next-day price direction of WTI crude oil by combining:

- regime signals from an unsupervised HMM
- macroeconomic and technical exogenous features
- CFTC/COT trader positioning data
- supervised models tailored for regime-aware performance

### Key Themes

- `Regime feature engineering`: The HMM is trained on market-state and macro indicators to produce discrete regime labels and regime probabilities. These regime outputs are used as features rather than as a final classifier.

- `Exogenous data`: CFTC/COT positioning and macro data are used to augment standard price and technical inputs. This helps capture market structure signals from trader behavior and broad economic conditions.

- `Multiple model families`: The repository compares several predictive approaches, including:
  - gradient boosting classifiers
  - extreme learning machines (ELM)
  - GRU sequence models
  - FAVAR models using latent factors from PCA and VAR

- `Regime-specific modeling`: The models are evaluated in a regime-aware setting, where regime features can be used to adapt predictions or inform regime-dependent model choices.

- `Trading strategy tuning`: A shared probability-based trading strategy is tuned across all model families to provide a consistent and comparable performance evaluation.

## What’s Included

### `HMM_regimes.ipynb`
- constructs regime labels and regime probabilities using a Gaussian HMM
- uses macro variables, price-derived state variables, and CFTC/COT data
- produces regime features for downstream forecasts

### `CFTC_WTI_2.ipynb`
- downloads and cleans CFTC/COT Commitment of Traders data
- filters for WTI crude oil futures contracts
- builds positioning and speculative pressure features for forecasting

### Model notebooks

Each supervised model notebook trains and evaluates a set of feature specifications:

- baseline macro/price features
- CFTC/COT-augmented features
- HMM regime-augmented features
- regime-specific feature/model variants

### `trading_strategy.ipynb`
- tunes a shared trading strategy using model probability outputs
- uses volatility-scaling and clipping for consistent position sizing
- evaluates performance across Gradient Boosting, ELM, GRU, and FAVAR predictions

## How to Use

1. Open the notebooks in `notebooks/` in Jupyter or JupyterLab.
2. Start with `CFTC_WTI_2.ipynb` to build the exogenous WTI feature set.
3. Run `HMM_regimes.ipynb` to generate regime features.
4. Explore each model notebook to compare forecasting performance and feature variants.
5. Finish with `trading_strategy.ipynb` to evaluate an end-to-end strategy.

## Recommended Workflow

1. Data preparation: `notebooks/CFTC_WTI_2.ipynb`
2. Regime feature engineering: `notebooks/HMM_regimes.ipynb`
3. Model training and evaluation: `notebooks/gradient_boosting_final_paper.ipynb`, `notebooks/ELM_final_paper.ipynb`, `notebooks/gru_final_paper.ipynb`, `notebooks/favar_final_paper.ipynb`
4. Trading strategy analysis: `notebooks/trading_strategy.ipynb`

## Notes

- The repository is intended as a complete final project package for a regime-aware commodity forecasting problem.
- The notebooks can be run sequentially for a reproducible research workflow.
- The final PDF report summarizes the methods, experiments, and results.
