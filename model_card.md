# Model Card: Bayesian Black-Box Optimisation System  
Imperial College London – ML/AI BBO Capstone Project  

---

## 1. Overview

### Model Name
Bayesian Black-Box Optimisation System (BBO-GP-EI-UCB)

### Type
Sequential Bayesian Optimisation framework  

### Version
v1.0 (Weeks 1–10 implementation, pre-validation stage)

---

## Description

This model performs **optimisation of unknown functions** using:
- Gaussian Process (GP) surrogate modelling  
- Acquisition-based query selection  

It operates under a strict constraint of:
- **One query per iteration**

---

## 2. Intended Use

### Suitable Tasks

- Black-box optimisation  
- Hyperparameter tuning  
- Simulation-based optimisation  
- Low-budget sequential problems  
- Noisy or expensive evaluations  

### Not Suitable For

- Safety-critical systems  
- One-shot optimisation problems  
- Deterministic analytical optimisation  
- Causal inference  

---

## 3. Model Strategy and Evolution

### Core Components

- Gaussian Processes (GPs)  
- RBF and Matérn kernels  
- Automatic Relevance Determination (ARD)  
- Acquisition functions:
  - Expected Improvement (EI)  
  - Upper Confidence Bound (UCB)  

### Optimisation Methods

- Multi-start optimisation  
- Differential Evolution (DE)  
- L-BFGS-B refinement  
- Random restarts and jitter  

---

### Strategy Evolution

| Phase | Weeks | Behaviour |
|------|------|----------|
| Exploration | 1–3 | Global search (high ξ / κ) |
| Balanced | 4–7 | Structure discovery |
| Localisation | 8–9 | Region refinement |
| Exploitation | 10 | Near-greedy EI, tight bounds |
| Validation | 11–12 | Confirm convergence, minimal exploration |

> **Note:** Exact queries, ξ/κ values, and search radii per function are detailed in the [main README](README.md) tables.

---

### Week 10 Behaviour

- EI uses very small ξ (0.0005–0.005)  
- Search radius ≈ 0.02–0.03  
- Strong reliance on GP posterior  

This reflects **provisional convergence**, not final confirmation. Weeks 11–12 address full validation.

---

## 4. Performance Summary

| Function | Outcome |
|----------|--------|
| F1 | Localised narrow peaks identified |
| F2 | Stable optimisation under noise |
| F3 | Sensitive dimension exploited |
| F4 | Multimodal optimisation handled via DE |
| F5 | Near-optimal convergence |
| F6 | Dimension-aware improvements |
| F7 | Gradual high-dimensional refinement |
| F8 | Ridge-following behaviour |

### Metrics

- Best observed value  
- Convergence trend  
- GP stability  
- Exploration vs exploitation balance (qualitative)  

---

## 5. Assumptions and Constraints

### Assumptions

- Local smoothness of functions  
- GP surrogate is adequate  
- Noise is approximately Gaussian  
- ARD correctly identifies important dimensions  

### Constraints

- One query per iteration  
- Limited evaluation budget  
- No access to true function  

---

## 6. Failure Modes

- Convergence to local optima  
- Overconfidence in GP predictions  
- Noise misinterpretation (F2)  
- Incorrect dimension relevance (ARD)  
- Boundary bias (high-dimensional functions)  

---

## 7. Transparency and Reproducibility

### Transparency

The system documents:
- Query history  
- Acquisition strategies  
- Kernel choices  
- Strategy evolution  

### Reproducibility

Reproducible at a **methodological level**, but requires:
- GP hyperparameters  
- Optimisation settings  
- Random seeds  
- Week-by-week queries and ξ/κ values are in the [main README](README.md) tables

### Adaptability

- Can be applied to new optimisation problems  
- Parameters (ξ, κ, bounds) can be tuned  
- Alternative acquisition strategies can be used  

---

## 8. Key Insight

> Early exploration determines the trajectory of optimisation, while late-stage performance depends on how effectively the model exploits learned structure.

---

## 9. Week 10 Context

- Optimisation is highly local  
- Improvements are diminishing  
- Model confidence is high but not fully validated  

Weeks 11–12 are required to:
- Confirm optimality  
- Test robustness  
- Address remaining uncertainty
