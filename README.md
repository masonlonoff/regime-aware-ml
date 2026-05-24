# Regime-Aware ML for WTI Direction Forecasting — What we did and why it matters

![WTI Crude Oil](https://bsmedia.business-standard.com/_media/bs/img/article/2024-10/03/full/1727978541-4907.jpg?im=FeatureCrop,size=(382,233))

This repository contains the final analysis and results for a regime-aware WTI (West Texas Intermediate) direction forecasting project. Below I explain the contributions, the intuition behind the methods, and why these choices improve robustness and interpretability.

## High-level contributions

- Built a robust regime feature set using a Gaussian Hidden Markov Model (HMM) trained on macro, price-state, and trader-positioning variables. This converts noisy continuous signals into concise regime labels and regime probabilities that capture market-state structure.

- Engineered exogenous features from CFTC/COT trader-positioning reports and macroeconomic indicators. These features provide behavioral and macro drivers of crude oil risk premia that are not captured by price history alone.

- Evaluated multiple supervised model families (Gradient Boosting, Extreme Learning Machine, GRU, FAVAR) across consistent feature sets to identify which modeling paradigms best leverage regime and exogenous information.

- Designed a single, shared trading strategy tuned on validation probabilities to compare model families fairly and assess economic significance beyond classification metrics.

## Why these choices are valuable

- Regime abstraction (HMM): Market dynamics are non-stationary. The HMM compresses structural changes into a small set of regimes, letting downstream models condition on market state instead of overfitting transient patterns. Regimes also enable regime-specific risk management and interpretation.

- Exogenous trader and macro features: CFTC/COT positioning summarizes cross-sectional trader behavior (hedgers, speculators) that often leads price moves rather than follows them. Macro indicators capture broader economic drivers. Together, these features improve signal-to-noise for short-horizon forecasting.

- Multiple model families: Different models capture different inductive biases. Tree-based models handle heterogeneous features and interactions; GRUs capture short temporal dependencies; ELMs provide a fast, regularized benchmark; FAVARs capture latent macro dynamics. Comparing them shows which biases exploit regime/exogenous structure best.

- Shared strategy for economic evaluation: Reporting returns from a single, well-specified trading rule ensures results are economically comparable and not an artifact of bespoke position sizing per model.

## Key empirical takeaways

- Regime features consistently improved forecasting performance across model families, reducing false signals during regime transitions and improving risk-adjusted returns.

- CFTC/COT features provided additive predictive value, especially when combined with regime probabilities — trader positioning signals often presage direction changes in relevant regimes.

- Simpler models (Gradient Boosting) often matched or outperformed more complex models after regime and exogenous features were introduced, suggesting that feature engineering + regime-awareness reduces the need for highly expressive architectures.

## How to interpret the notebooks

- `notebooks/HMM_regimes.ipynb` explains how regimes were constructed and validated. Inspect the regime-transition matrices and feature importance to understand what economic states each regime represents.

- `notebooks/CFTC_WTI_2.ipynb` describes the construction of trader-positioning features and common pitfalls (look-ahead bias, contract filtering).

- Model notebooks document experiments comparing feature sets and models; focus on the comparative tables and the trading-strategy P&L summaries for practical implications.

## Limitations and caveats

- The analysis focuses on next-day direction; performance may vary for other horizons.
- Results depend on the specific time period and available macro/COT coverage.
- Full retraining and evaluation require the data pipelines described in the notebooks and may be computationally intensive.

## Author

- Mason Lonoff
