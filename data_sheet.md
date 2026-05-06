# Black Box Optimisation (BBO) Datasheet  
Imperial College London – ML/AI BBO Capstone Project  

---

## 1. Motivation

This datasheet was created to support the study of **sequential black-box optimisation under limited evaluation budgets**.

The task is to **maximise eight unknown objective functions** using only observed input–output pairs, without access to the underlying mathematical form. This reflects real-world problems where evaluations are expensive or opaque.

The dataset supports:
- Bayesian Optimisation research  
- Sequential decision-making under uncertainty  
- Exploration–exploitation trade-off analysis  

---

## 2. Composition

### Functions

| Function | Dim | Characteristics |
|----------|-----|----------------|
| F1 | 2D | Deterministic, sparse peaks |
| F2 | 2D | Noisy, multimodal |
| F3 | 3D | Transformed objective (side-effect minimisation) |
| F4 | 4D | Multimodal hyperparameter tuning |
| F5 | 4D | Unimodal, smooth |
| F6 | 5D | Structured with dimension sensitivity |
| F7 | 6D | High-dimensional, partially structured |
| F8 | 8D | Complex, multimodal, ridge-like |

---

### Size

- 8 independent datasets (one per function)  
- Sequential observations collected over **13 weeks**  
- **1 query per function per week**  
- Dataset grows incrementally over time  

---

### Format

- Inputs are n-dimensional vectors: `x = [x1, x2, ..., xn]`, xi ∈ [0,1], stored as hyphen-separated strings x1-x2-...-xn rounded to six decimal places (e.g., `0.123456-0.654321`).  
- Outputs are scalar values: `y ∈ ℝ`, representing function evaluations. 

---

### Gaps and Limitations

- Sparse sampling due to strict query budget  
- Increasing concentration of samples near optima (Weeks 8–13)  
- Large areas of the search space remain unexplored  
- High-dimensional functions (F7–F8) are only partially covered  

---

## 3. Collection Process

### Method

Data was generated using **sequential Bayesian Optimisation**:

1. Fit a Gaussian Process (GP) surrogate model  
2. Select next query via an acquisition function  
3. Evaluate the function and update dataset  

---

### Strategy Over Time

| Phase | Weeks | Strategy |
|------|------|----------|
| Exploration | 1–3 | Broad search (high ξ / κ) |
| Mixed | 4–7 | Exploration + exploitation |
| Localisation | 8–9 | Focus near promising regions |
| Exploitation | 10–13 | Tight local refinement; Weeks 11–13 for convergence and final confirmation |

> **Note:** Exact queries, ξ/κ values, and search radii per function are detailed in the [main README](README.md) tables.

---

### Techniques Used

- Gaussian Processes (GPs)  
- RBF / Matérn kernels with ARD  
- Expected Improvement (EI)  
- Upper Confidence Bound (UCB)  
- Multi-start optimisation  
- Differential Evolution  
- Adaptive bounds tightening  

---

### Time Frame

- Data collected over **13 weeks**
- Week 10 represents **advanced-stage exploitation**, Weeks 11–13 focus on **validation and convergence confirmation**  

---

## 4. Preprocessing and Transformations

- Log transformation applied for stability  
- Output shifting applied for negative objectives  
- Inputs remain bounded in [0,1]  
- No missing values  
- No scaling beyond [0,1] normalisation  

---

## 5. Uses

### Intended Uses

- Bayesian optimisation research  
- Sequential learning experiments  
- Surrogate modelling  
- Educational coursework  

### Inappropriate Uses

- Real-world decision-making (medical, financial, etc.)  
- Safety-critical systems  
- Causal inference tasks  

This dataset allows researchers and participants to replicate the sequential optimisation methodology in a controlled setting.

---

## 6. Distribution and Access

- Available via this GitHub repository in the file `full_data_inputs_and_outputs.md`.
- Terms of Use: Educational and research use only. Not for commercial deployment.
- Reproducibility Note: All input-output datasets (Weeks 1–13) are included, enabling full reproducibility of the optimisation experiments. The underlying functions remain unknown (black-box setting), but week-by-week queries allow replication of the methodological process.

---

## 7. Maintenance

- Maintained and updated by the project author during Weeks 1–13  
- Final version included in the repository is frozen and complete

---

## 8. Ethical Considerations

- No personal or sensitive data; fully synthetic  
- Highlights risks of:
  - Over-exploitation of search space  
  - Model overconfidence  
  - Limited exploration in some regions

---

## 9. Key Limitation

The dataset reflects a **path-dependent optimisation process**, where:
- Early sampling decisions strongly influence later results  
- Some regions may never be explored  
- Weeks 11–13 mainly serve to validate convergence and final optima
