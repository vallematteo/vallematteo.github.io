# Method-Oriented Calibration for Economic ABMs

## Classical Economic Simulation Methods

### 1. Indirect Inference
**Authors**: Gourieroux, C., Monfort, A., & Renault, E. (1993)  
**Link**: https://onlinelibrary.wiley.com/doi/abs/10.1002/jae.3950080507

**Method**: Use auxiliary model to match moments; choose parameters so auxiliary estimates from simulated and real data are close.

**Why it works**: Achieves consistent estimation even when auxiliary model is misspecified, as long as structural parameters have independent effects on auxiliary parameters.

**Best for**: Dynamic economic models, DSGE-like ABMs, continuous-time models.

**Data types**: Moments from empirical time-series; cross-sectional moments.

---

### 2. Simulated Method of Moments (SMM)
**Authors**: McFadden, D. (1989); Pakes, A., & Pollard, D. (1989)  
**Link**: https://opensourceecon.github.io/CompMethods/struct_est/SMM.html

**Method**: Match moments (e.g., mean, variance, autocorrelation) from simulated data to observed data via optimization.

**Why it works**: Consistent and asymptotically normal estimator under identifiability conditions (order: #moments ≥ #parameters; rank: parameters differentially affect moments).

**Best for**: Heterogeneous-agent models, financial market ABMs, any model where likelihood is intractable.

**Data types**: Empirical moments from time-series or cross-sectional data.

---

### 3. On the Problem of Calibrating an Agent-Based Model for Financial Markets
**Authors**: Fabretti, A. (2013)  
**Link**: https://link.springer.com/article/10.1007/s11403-012-0096-3

**Method**: Combine Nelder-Mead simplex algorithm with threshold-accepting heuristic and genetic algorithms to calibrate Farmer-Joshi ABM; minimize distance between simulated and empirical moments.

**Why it works**: Handles non-smooth, multi-modal objective functions; genetic algorithms escape local minima better than gradient-based methods; explicitly accounts for Monte Carlo variance in objective function.

**Best for**: Financial market ABMs with many parameters and complex loss landscapes; applies to moment-matching calibration with stylized facts.

**Data types**: Financial time-series moments (returns, volatility, autocorrelation); empirical moments from real market data.

---

### 4. Efficient Calibration of a Financial Agent-Based Model Using the Method of Simulated Moments
**Authors**: (Recent application showing computational efficiency improvements)  
**Link**: https://link.springer.com/chapter/10.1007/978-3-030-77967-2_27

**Method**: SMM with filtered neighborhood optimization to reduce computational cost while maintaining accuracy.

**Why it works**: Gradually narrows search space by examining local neighborhoods, exploiting structure of objective surface.

**Best for**: Large parameter spaces; computationally expensive financial ABMs.

**Data types**: Financial moments (returns, volatility, autocorrelation, fat tails).

---

## Bayesian Approaches

### 5. Bayesian Calibration of Computer Models
**Authors**: Kennedy, M. C., & O'Hagan, A. (2001)  
**Link**: https://www.asc.ohio-state.edu/statistics/comp_exp//jour.club/kennedy01.pdf

**Method**: Model computer output as Gaussian process with explicit discrepancy term δ(x); use Bayesian inference to estimate parameters and model inadequacy.

**Why it works**: Quantifies both parameter uncertainty AND model discrepancy; accounts for the fact that no model is perfect.

**Best for**: Continuous parameter spaces; when you have both empirical data and want full uncertainty quantification.

**Data types**: Pointwise empirical observations; works with expensive-to-evaluate models.

---

### 6. Bayesian Estimation of Agent-Based Models via Adaptive Particle Markov Chain Monte Carlo
**Authors**: (Recent, 2021)  
**Link**: https://link.springer.com/article/10.1007/s10614-021-10155-0

**Method**: Use adaptive particle MCMC to sample from posterior distribution of parameters given observed data.

**Why it works**: Particle methods handle multimodal posteriors better than standard MCMC; adapts proposal distributions on-the-fly.

**Best for**: ABMs with moderate parameter counts; when you need full posterior distribution, not just point estimates.

**Data types**: Time-series data; likelihood-free inference using summary statistics.

---

### 7. Black-Box Bayesian Inference for Agent-Based Models
**Authors**: Dyer, J., Cannon, P., Farmer, J.D., & Schmon, S.M. (2024)  
**Link**: https://www.sciencedirect.com/science/article/pii/S0165188924000198  
**Preprint**: https://arxiv.org/abs/2202.00625

**Method**: Use neural networks to learn direct mapping from data to posterior distribution (neural posterior estimation and neural density ratio estimation); applies simulation-based inference.

**Why it works**: Avoids explicit likelihood; learns posterior from ensemble of simulations; amortizes cost across many observations; achieves accurate posteriors with orders of magnitude fewer simulations than traditional methods.

**Best for**: Very high-dimensional parameter spaces; when summary statistics are difficult to define; computationally expensive economic ABMs.

**Data types**: Any type of data including multivariate time-series; works with neural network emulators.

---

## Approximate Likelihood-Free Methods

### 8. Calibration and Evaluation of Individual-Based Models Using Approximate Bayesian Computation
**Authors**: Hartig, F., Calabrese, J. M., Reineking, B., Wiegand, T., & Huth, A. (2011)  
**Link**: https://www.sciencedirect.com/science/article/pii/S0304380015002173

**Method**: ABC: generate simulations under various parameters, accept those matching observed data within tolerance ε; use accepted simulations to estimate posterior.

**Why it works**: Works without likelihood function; asymptotic acceptance region gives valid Bayesian posterior (within tolerance).

**Best for**: Stochastic economic ABMs; high-dimensional parameter spaces; when summary statistics capture essential features.

**Data types**: Summary statistics from observed data.

---

### 9. Likelihood-Free Inference by Ratio Estimation
**Authors**: (Recent neural simulation-based inference)  
**Link**: https://arxiv.org/pdf/1611.10242

**Method**: Train neural network classifier to estimate likelihood-to-marginal ratio p(data|θ)/p(data); use for inference.

**Why it works**: Avoids density estimation; directly learns the relevant ratio for inference.

**Best for**: Economic ABMs with expensive simulations; combines with sequential refinement for efficiency.

**Data types**: Summary statistics; raw simulation outputs.

---

## Machine Learning / Surrogate-Based Methods

### 10. Agent-Based Model Calibration using Machine Learning Surrogates
**Authors**: Lamperti, F., Roventini, A., & Sani, A. (2018)  
**Link**: https://arxiv.org/abs/1703.10639

**Method**: Train neural network or Gaussian process to emulate ABM; calibrate using surrogate instead of true model; expensive simulations only for training.

**Why it works**: Reduces computational cost by orders of magnitude; maintains uncertainty quantification; allows efficient exploration of parameter space.

**Best for**: Computationally expensive macro ABMs (EURACE-style); large parameter spaces.

**Data types**: Empirical moments; macro time-series data; trained on simulation ensemble.

---

### 11. Using Machine Learning as a Surrogate Model for Agent-Based Simulations
**Authors**: Lamperti, F., Roventini, A., & Sani, A. (2022)  
**Link**: https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0263150

**Method**: Compare ANNs, gradient-boosted trees, and GPs as surrogates; optimize via calibration on surrogate.

**Why it works**: Demonstrates which surrogates best preserve ABM behavior for different output types; guides method selection.

**Best for**: Any large ABM; practical guidance on which ML method to use.

**Data types**: Simulation training data; empirical targets.

---

## Pattern-Based Calibration

### 12. Pattern-Oriented Modelling: A 'Multi-Scope' for Predictive Systems Ecology
**Authors**: Grimm, V., & Railsback, S. F. (2012)  
**Link**: https://royalsocietypublishing.org/doi/abs/10.1098/rstb.2011.0180

**Method**: Identify patterns at multiple scales/hierarchies; calibrate to reproduce *all* patterns simultaneously; discard parameter sets failing any pattern.

**Why it works**: Multi-criteria calibration reduces overfitting risk; validates mechanisms at different scales; patterns constrain parameter space more than single moment.

**Best for**: Macro ABMs; when you have multiple stylized facts at different organizational levels.

**Data types**: Categorical/qualitative patterns; stylized facts; multi-scale observations.

---

## Validation Framework

### 13. Validation of Agent-Based Models in Economics and Finance
**Authors**: Fagiolo, G., Guerini, M., Lamperti, F., Moneta, A., & Roventini, A. (2017)  
**Link**: https://www.econstor.eu/bitstream/10419/174573/1/2017-23.pdf

**Method**: Framework comparing three calibration/validation paradigms: (i) stylized facts matching, (ii) moment matching (SMM), (iii) econometric testing.

**Why it works**: Clarifies *when* each approach is appropriate; shows trade-offs between statistical rigor and computational efficiency.

**Best for**: Understanding methodological choice; identifying which approach suits your economic ABM's purpose.

**Data types**: Empirical moments; econometric test statistics; stylized facts.

---

## Quick Method Selection Guide

| **Model Type** | **Primary Method** | **Alternative** |
|---|---|---|
| **Macro ABM (expensive)** | Surrogates (10, 11) + SMM | ABC (8) |
| **Financial market ABM** | SMM with evolutionary opt. (2, 3) | Bayesian MCMC (6) |
| **High-parameter ABM** | Pattern-oriented (12) | Surrogate + ABC (10+8) |
| **Stochastic economic ABM** | ABC (8) or indirect inference (1) | Bayesian (5, 6) |
| **Policy-focused ABM** | Moment matching (2) validated with patterns (12) | Surrogate forecasting (10) |
| **Very high-dimensional ABM** | Neural SBI (7) | Surrogates + SMM (10+2) |

---

## Notes

- All 13 papers are **method-focused**—each explains a specific calibration/inference technique and *why* it works for economic ABMs
- Papers are ordered from classical to modern approaches
- Paper 7 (Dyer et al., 2024) represents the cutting edge of simulation-based inference for ABMs using neural networks
