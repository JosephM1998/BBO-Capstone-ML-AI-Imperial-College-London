# Model Card: Bayesian Black-Box Optimisation System
**Imperial College London – ML/AI BBO Capstone Project**

---

## 1. Overview
**Model Name:** Bayesian Black-Box Optimisation System (BBO-GP-EI-UCB) 
**Type:** Sequential Bayesian Optimisation framework 
**Version:** v1.1 (Weeks 1–13, including final validation and convergence)

**Description:** 
The system performs optimisation of unknown black-box functions by sequentially selecting input points and learning from previous evaluations. It uses:

- Gaussian Process (GP) surrogate modelling 
- Acquisition functions: Expected Improvement (EI), Upper Confidence Bound (UCB) 

It operates under a strict **one query per function per week** regime over 13 weeks, reflecting realistic cost constraints.

---

## 2. Intended Use
**Suitable Tasks:** 
- Black-box optimisation 
- Hyperparameter tuning 
- Simulation-based optimisation 
- Low-budget sequential problems 
- Noisy or expensive evaluations 

**Not Suitable For:** 
- Safety-critical systems 
- One-shot optimisation 
- Deterministic analytical optimisation 
- Causal inference tasks 

---

## 3. Model Strategy and Evolution
**Core Components:** 
- Gaussian Processes (GPs) with RBF / Matérn kernels and Automatic Relevance Determination (ARD) 
- Acquisition strategies: EI and UCB, tuned per function and phase 
- Optimisation methods: Multi-start, Differential Evolution (DE), L-BFGS-B refinement, random restarts 

**Strategy Timeline:** 

| Phase | Weeks | Behaviour |
|----------------|-------|-----------------------------------------------|
| Exploration | 1–5 | Broad global search; moderate ξ/κ; LHS for high-dimensional functions |
| Exploitation + Some Exploration | 6–9 | Focus on promising regions; ARD identifies sensitive dimensions; DE/multi-start avoids local traps |
| Final Exploitation | 10 | Tight local refinement near best-known optima; ξ very small; boundary effects important |
| Convergence & Confirmation | 11–13 | Minimal exploration; GP predictions trusted; final evaluations confirm reproducibility |

**Notes:** 
- Weeks 11–13 provide final confirmation and consolidation of function behaviour. 
- ξ/κ values progressively decrease to ensure convergence. 
- Transformations (log/shift) stabilise GP predictions, especially for negative or noisy outputs.

---

## 4. Performance Summary

| Function | Outcome |
|----------|---------|
| F1 | Localised narrow peaks identified; final validation confirms convergence | 
| F2 | Stable optimisation under noise; final maxima confirmed | 
| F3 | Sensitive dimensions exploited; drug-combo candidates refined | 
| F4 | Multimodal ML hyperparameter tuning handled; DE ensures reproducibility | 
| F5 | Near-optimal convergence; ultra-precise final yield | 
| F6 | Dimension-aware recipe improvements; ARD confirms relevant features | 
| F7 | High-dimensional refinement; final queries ensure convergence |
| F8 | Ridge-following behaviour in complex 8D space; boundaries confirmed |

**Metrics Used:** 
- Best observed values per function 
- Convergence trends over weeks 
- GP surrogate stability 
- Qualitative exploration vs exploitation balance 

---

## 5. Assumptions and Constraints
**Assumptions:** 
- Local smoothness of functions 
- GP surrogate adequately models function behaviour 
- Noise approximately Gaussian for stochastic functions 
- ARD correctly identifies sensitive dimensions 

**Constraints:** 
- One query per function per week 
- Limited evaluation budget 
- No access to true function 
- Function dimensionality varies (2D–8D), some with noise or complex interactions 

---

## 6. Failure Modes
- Convergence to local optima 
- Overconfidence in GP predictions 
- Noise misinterpretation (F2) 
- Incorrect dimension relevance (ARD) 
- Boundary bias for high-dimensional functions (F7, F8) 

---

## 7. Transparency and Reproducibility
**Transparency:** 
- Week-by-week query history, acquisition function choices, kernel selections, and strategy evolution documented in notebooks 
- All EI/UCB parameters, bounds, and GP hyperparameters included 

**Reproducibility:** 
- Full dataset: [`full_data_inputs_and_outputs.md`](./full_data_inputs_and_outputs.md) 
- Notebooks: [`/notebooks/Module 12-24 BBO Capstone.ipynb`](./notebooks) 
- Allows replication of sequential optimisation methodology and convergence confirmation 

**Adaptability:** 
- Can be applied to new black-box problems 
- Acquisition strategies, ξ/κ, and bounds tunable per function 
- Optional transformations for stabilisation 

---

## 8. Key Insight
- Early exploration determines the trajectory of optimisation 
- Mid-phase exploitation leverages learnt structure 
- Late-phase convergence (Weeks 11–13) validates optima and ensures reproducibility 
- ARD identifies sensitive dimensions, guiding efficient local refinement 

---

## 9. Non-Technical Summary
This model optimises unknown functions by learning from sequentially collected data. Each week, it selects one input to evaluate, balancing the search between unexplored regions and promising peaks. Across 13 weeks, it transitions from broad exploration to fine-grained exploitation, culminating in reproducible near-optimal solutions for all eight functions. It is suitable for research, simulations, and coursework, but not for real-world safety-critical decision-making. Full datasets and notebooks allow anyone to replicate the experiments and verify results.

---

## 10. References
- Rasmussen & Williams (2006), *Gaussian Processes for Machine Learning* 
- Jones et al. (1998), *Efficient Global Optimization* 
- Imperial College London Professional Certificate in ML/AI materials

