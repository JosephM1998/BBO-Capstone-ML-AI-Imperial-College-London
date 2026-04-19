# Black Box Optimisation (BBO) Capstone Project - Imperial College London ML/AI Course

## Section 1: Project Overview

The Black-Box Optimisation (BBO) capstone project simulates a realistic machine learning scenario where the underlying system is unknown and data is limited. Participants are given eight synthetic black-box functions (ranging from 2D to 8D) and must optimise them without access to their true form.

The objective is to maximise each function’s output using a sequential decision-making process with only one query per function per week. This constraint reflects real-world settings where evaluations are expensive, such as hyperparameter tuning, scientific experimentation, or engineering design.

The project emphasises:
- Balancing exploration and exploitation
- Learning from sparse and noisy observations
- Updating models iteratively as new data becomes available
- Making uncertainty-aware decisions

This setting mirrors real-world optimisation challenges in machine learning, where the objective function is unknown and costly to evaluate. As a result, the project develops practical skills in:
- Bayesian optimisation
- Model tuning under uncertainty
- Identifying relevant vs irrelevant features
- Avoiding overfitting in low-data regimes

---

## Function Descriptions

The eight functions represent different real-world optimisation scenarios:

| Function | Dim | Description |
|----------|-----|------------|
| F1 | 2D | Detect contamination sources with sparse, localised signals |
| F2 | 2D (noisy) | Optimise a noisy likelihood function with multiple local optima |
| F3 | 3D | Drug discovery: minimise side effects via transformed objective |
| F4 | 4D | Warehouse optimisation via ML surrogate model tuning |
| F5 | 4D | Chemical process optimisation (unimodal yield function) |
| F6 | 5D | Recipe optimisation with multiple competing objectives |
| F7 | 6D | ML hyperparameter tuning (unknown performance landscape) |
| F8 | 8D | High-dimensional optimisation with complex interactions |

These functions vary in dimensionality, noise, and structure, requiring different optimisation strategies and highlighting the challenges of black-box optimisation in practice.

--- 

## Section 2: Navigating this repository



## Section 3: Inputs and Outputs

### Inputs
The dataset consists of eight independent sets of input query vectors corresponding to Functions 1–8, with dimensionality ranging from 2D to 8D.

- Each query is a vector:  
  **x = [x₁, x₂, …, xₙ]**, where *n ∈ {2,…,8}*
- Each component lies within a bounded domain:  
  **xᵢ ∈ [0, 1]**
- Queries are recorded in a hyphen-separated format with fixed precision (6 decimal places), for example:  
  `0.123456-0.789876` (2D)

A strict evaluation constraint applies:
- **One query per function per week**
- This results in a **small, sequentially growing dataset**

---

### Outputs
Each query produces a single scalar output:

- **y ∈ ℝ** (can be positive or negative)
- Represents the performance or objective value of the function
- Some functions include noise or transformations (e.g. negation, log-scaling)

Each input–output pair forms one observation used to update the optimisation model.

## Section 4: Challenge Objectives

The goal of the BBO capstone project is to maximise the outputs of eight unknown black-box functions using only sequentially acquired data.

Since the functional forms are hidden, optimisation must rely entirely on:
- Observed input–output pairs
- Surrogate modelling (e.g. Gaussian Processes)
- Intelligent search strategies balancing exploration and exploitation

---

### Constraints

The optimisation problem is deliberately designed to reflect real-world limitations:

- **Limited query budget:** one submission per function per week  
- **Delayed feedback:** outputs are revealed only after each weekly cycle  
- **Varying dimensionality:** functions range from 2D to 8D  
- **Noise:** some functions include stochastic outputs  
- **Non-linearity:** highly complex and multi-modal landscapes  

These constraints make traditional analytical or gradient-based optimisation infeasible.

---

### Implications

As a result, the task requires:
- Careful management of uncertainty  
- Efficient use of sparse data  
- Adaptive strategies that evolve over time  

This setup mirrors real-world optimisation problems such as hyperparameter tuning, scientific experimentation, and engineering design, where evaluations are costly and limited.

---

## Section 5: Technical Approach

This section summarises the approach taken across 12 weeks for the Black-Box Optimisation (BBO) capstone project. All eight functions are maximisation tasks. The strategies evolved from exploration-focused early weeks to exploitation-focused later weeks.

---

### Weeks 1–5: Exploration Phase
- **Goal:** Discover promising regions of the unknown functions while avoiding premature convergence.
- **Strategy:**  
  - Used Expected Improvement (EI) with moderate ξ or Upper Confidence Bound (UCB) with moderate κ.  
  - Adjusted acquisition functions per function based on dimensionality, noise, and landscape complexity.  
  - Multi-start or Latin Hypercube Sampling (LHS) for higher-dimensional or multimodal functions.  
  - Gaussian Process (GP) kernels adapted per function, with log/shift transforms applied where necessary for stability.

| Function | Weeks 1–5 Approach | Rationale |
|----------|-----------------|----------|
| F1 (2D) | EI ξ=0.05 → UCB κ=2.5 → EI ξ=0.1 → UCB κ=6 → UCB κ=6 | Conservative start, then more exploration; log-transform maintained for narrow peaks |
| F2 (2D, noisy) | EI ξ=0.1 → UCB κ=2.5 → EI ξ=0.15 → UCB κ=4.5 → UCB κ=3.8 | Noise-aware EI/UCB alternation; broaden exploration then refine local peaks |
| F3 (3D) | EI ξ=0.1 → UCB κ=2.5 → UCB κ=3.0 → UCB κ=2.5 → Multi-start EI ξ=0.03 | Increased κ to push exploration in sensitive dimensions; negative outputs shifted |
| F4 (4D) | EI ξ=0.2 → UCB κ=2.5 → UCB κ=5.0 + DE → UCB κ=4 + DE → UCB κ=3.8 + DE | High κ + jitter avoids boundary collapse; DE ensures diverse exploration |
| F5 (4D, unimodal) | EI ξ=0.1 → UCB κ=2.5 → UCB κ=2.5 + random search → UCB κ=2.5 → EI ξ=0.01 | Focused exploration near known peak; random search supports robustness |
| F6 (5D) | EI ξ=0.1 → UCB+penalty κ=2.0 → UCB+penalty κ=3.5 → UCB+penalty κ=2.5 → UCB+penalty κ=1.2 | Penalties + distance heuristics avoid poor regions; explore key ingredients |
| F7 (6D) | EI ξ=0.1 → UCB κ=5.0 → UCB κ=5.0 → UCB κ=1.5 → UCB κ=1.3 | High κ initially to explore high dimensions; boundary-safe adjustments later |
| F8 (8D) | EI ξ=0.2 → EI ξ=0.2 → LHS + UCB κ=8 → LHS + UCB κ=7 → LHS + UCB κ=6 | Latin Hypercube Sampling + UCB ensures global exploration and dimension coverage |

---

### Weeks 6–9: Exploitation Phase
- **Goal:** Focus on refining the promising regions discovered earlier, with limited exploration where needed.  
- **Strategy:**  
  - Tight local bounds around best-known optima.  
  - EI with small ξ for exploitation; sometimes hybrid EI+UCB for noise handling.  
  - Differential Evolution (DE) or multi-start EI to avoid local traps in multimodal or rugged landscapes.  
  - Automatic Relevance Determination (ARD) kernels to prioritise sensitive dimensions.  
  - Transformations (log/shift) applied to stabilise GP predictions.  
  - PCA visualisations for functions ≥4D to ensure query points remain in optimal clusters.

---

### Week 10: Final Exploitation
| Function | Dim | Focus | Query | EI ξ / Search Radius | Notes |
|----------|-----|-------|-------|--------------------|-------|
| F1 | 2D | Exploit best-known peak | [0.629953, 0.486520] | 0.005 / 0.02 | Narrow peaks, local refinement, no exploration needed |
| F2 | 2D | Refine local peak | [0.533026, 0.565895] | 0.005 / 0.02 | Noise-sensitive, careful GP exploitation |
| F3 | 3D | Refine promising drug combo | [0.869309,0.567474,0.093237] | 0.005 / focused bounds | Exploit low length-scale dimensions; negative outputs shifted |
| F4 | 4D | Local ML hyperparameter refinement | [0.401766,0.385109,0.392801,0.432944] | 0.003 / ±0.02 | DE avoids duplicates; focus on local cluster |
| F5 | 4D | Ultra-precise fine-tune | [0.999992,0.999997,0.999996,0.990008] | 0.0005 / tight bounds | Essentially pure exploitation |
| F6 | 5D | Refine recipe | [0.374036,0.285500,0.745577,0.848678,0.130795] | 0.0005 / ±0.03 | ARD highlights sensitive dims; slight boundary shifts |
| F7 | 6D | Local BO step | [0.1482,0.1625,0.3973,0.2662,0.2852,0.8291] | 0.001 / 0.02 | Local refinement; minor radius adjustments suggested |
| F8 | 8D | Ridge + boundary push | [0.0358,0.0832,0.1629, ~0,0.7542,0.4736,0.1572,0.8728] | 0.001 / 0.03 | High-dimensional boundary effects; minimal improvement |

**Key Patterns:**
- Exploitation dominates; ξ values very small.  
- Boundary behaviour important in high dimensions.  
- ARD identifies critical dimensions; lower length-scales → higher sensitivity.  
- Transformations stabilise GP predictions.  
- DE, multi-start, or L-BFGS-B used to avoid local traps.  
- PCA confirms points remain within optimal clusters.

---

### Weeks 11–12: Convergence and Confirmation (planned)

| Function | Dim | Planned Focus | Query | EI ξ / Search Radius | Notes |
|----------|-----|---------------|-------|--------------------|-------|
| F1 | 2D | Confirm best contamination source | – | – | Minimal exploration; trust GP; final validation |
| F2 | 2D | Confirm local peak refinement | – | – | Noise-aware; final check of previous maxima |
| F3 | 3D | Refine promising drug combination | – | – | Exploit sensitive dims; confirm stability of predictions |
| F4 | 4D | Validate ML hyperparameter refinement | – | – | Ensure DE results reproducible; local cluster confirmed |
| F5 | 4D | Ultra-precise final chemical yield | – | – | Near-peak evaluation; essentially pure exploitation |
| F6 | 5D | Confirm recipe optimisation | – | – | Check ARD-sensitive dimensions; slight boundary shifts if needed |
| F7 | 6D | Fine-tune hyperparameters | – | – | Local refinement; ensure reproducibility of BO steps |
| F8 | 8D | Validate ridge + boundary convergence | – | – | High-dimensional boundary effects; confirm minimal improvement |

**Key Points (planned):**
- No new queries yet; Weeks 11–12 will mainly confirm convergence.  
- Minimal exploration; GP predictions trusted for final evaluations.  
- Outcomes expected: reproducible results and complete understanding of function behaviour.

## Key Takeaways

- **Weeks 1–4 (Exploration):** Critical for discovering promising regions while avoiding premature convergence.  
- **Week 5 (Exploration-heavy):** Extends discovery phase, balancing exploration and beginning early refinement.  
- **Weeks 6–9 (Exploitation + Some Exploration):** Focus on high-potential regions; Gaussian Processes guide local searches; ARD identifies sensitive dimensions; Differential Evolution and multi-start strategies avoid local traps.  
- **Week 10 (Final Exploitation):** Tight local refinement near best-known optima; EI ξ very small; boundary and dimensional effects become important; transformations stabilize GP predictions.  
- **Weeks 11–12 (Convergence & Confirmation, planned):** Minimal exploration; trust GP predictions; final evaluations validate reproducibility and consolidate insights into function behaviour.

## Conclusion

- Week 10 marks late-stage convergence: improvements are incremental, and optima cluster tightly.  
- Weeks 11–12 will confirm convergence, ensuring reproducible results across all functions.  
- The optimisation strategy is consistent: explore early, refine mid-stage, exploit late, and validate at the end.  
- The repository demonstrates practical black-box optimisation under realistic constraints, balancing sequential decision-making, surrogate modelling, and uncertainty-aware strategies.

## Summary

This repository provides a complete end-to-end study of constrained black-box optimisation, combining:

- Sequential decision-making  
- Gaussian Process modelling  
- Acquisition-based search strategies  
- Realistic uncertainty-driven optimisation dynamics  

It serves as a practical demonstration of how ML systems operate when data is limited, expensive, and sequentially acquired.

## References
- Rasmussen & Williams (2006), "Gaussian Process for Machine Learning".
- Jones et. al (1998), "Efficient Global Optimization".
- Imperial College London Professional Certificate in ML/AI materials.
