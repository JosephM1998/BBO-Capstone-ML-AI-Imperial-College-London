# Black Box Optimisation (BBO) Capstone Project - Imperial College London ML/AI Course

## Section 1: Project Overview

The BBO capstone project simulates a realistic ML scenario where the underlying system is unknown and data is limited. Participants are given eight synthetic black‑box functions, ranging from 2D to 8D, and must optimise them without ever seeing their equations or shapes. Its purpose is to develop strategic, evidence‑driven optimisation skills through iterative experimentation.

The goal is to maximise each black‑box function’s output. Participants must rely on intelligent search strategies—balancing exploration and exploitation—to learn from limited observations. This reflects real‑world ML problems such as hyperparameter tuning, where the true objective function is unknown, and each evaluation is costly. The aim is to practise uncertainty‑aware decision‑making by updating models as new evidence arrives, managing noisy data, and refining strategies.

The project builds practical skills that transfer to real ML and data‑science work. It reinforces how to deal with uncertainty, overfitting, recognising irrelevant features, and tuning models effectively when data is scarce. It also develops an iterative, experimental mindset—testing ideas, analysing results, and adapting strategies. These skills are essential for my future career as an ML Engineer or Data Scientist using ML and AI.

### Descriptions of functions (this table is from Imperial College London ML/AI course material) 
| Function | Input X | Output y | Optimisation goal | Descriptions of sample applications |
|----------|-------|--------|-------------------|-------------------------------------|
| F1       | 2D Numpy array | 1D Numpy array | Maximise | Detect likely contamination sources in a two-dimensional area, such as a radiation field, where only proximity yields a non-zero reading. The system uses Bayesian optimisation to tune detection parameters and reliably identify both strong and weak sources. |
| F2       | 2D Numpy array | 1D Numpy array | Maximise | Imagine a black box, or a mystery ML model, that takes two numbers as input and returns a log-likelihood score. Your goal is to maximise that score, but each output is noisy, and depending on where you start, you might get stuck in a local optimum. To tackle this, you use Bayesian optimisation, which selects the next inputs based on what it has learned so far. It balances exploration with exploitation, making it well suited to noisy outputs and complex functions with many local peaks. |
| F3       | 3D Numpy array | 1D Numpy array | Maximise | You’re working on a drug discovery project, testing combinations of three compounds to create a new medicine. Each experiment is stored in initial_inputs.npy as a 3D array, where each row lists the amounts of the three compounds used. After each experiment, you record the number of adverse reactions, stored in initial_outputs.npy as a 1D array. Your goal is to minimise side effects; in this competition, it is framed as maximisation by optimising a transformed output (e.g. the negative of side effects). |
| F4       | 4D Numpy array | 1D Numpy array | Maximise | Address the challenge of optimally placing products across warehouses for a business with high online sales, where accurate calculations are costly and only feasible biweekly. To speed up decision-making, an ML model approximates these results within hours. The model has four hyperparameters to tune, and its output reflects the difference from the expensive baseline. Because the system is dynamic and full of local optima, it requires careful tuning and robust validation to find reliable, near-optimal solutions. |     
| F5       | 4D Numpy array | 1D Numpy array | Maximise | You’re tasked with optimising a four-variable black-box function that represents the yield of a chemical process in a factory. The function is typically unimodal, with a single peak where yield is maximised. Your goal is to find the optimal combination of chemical inputs that delivers the highest possible yield, using systematic exploration and optimisation methods. |
| F6       | 5D Numpy array | 1D Numpy array | Maximise | You’re optimising a cake recipe using a black-box function with five ingredient inputs, for example flour, sugar, eggs, butter and milk. Each recipe is evaluated with a combined score based on flavour, consistency, calories, waste and cost, where each factor contributes negative points as judged by an expert taster. This means the total score is negative by design. To frame this as a maximisation problem, your goal is to bring that score as close to zero as possible or, equivalently, to maximise the negative of the total sum. |
| F7       | 6D Numpy array | 1D Numpy array | Maximise | You’re tasked with optimising an ML model by tuning six hyperparameters, for example learning rate, regularisation strength or number of hidden layers. The function you’re maximising is the model’s performance score (such as accuracy or F1), but since the relationship between inputs and output isn’t known, it’s treated as a black-box function. Because this is a commonly used model, you might benefit from researching best practices or literature to guide your initial search space. Your goal is to find the combination of hyperparameters that yields the highest possible performance. |
| F8       | 8D Numpy array | 1D Numpy array | Maximise | You’re optimising an eight-dimensional black-box function, where each of the eight input parameters affects the output, but the internal mechanics are unknown. Your objective is to find the parameter combination that maximises the function’s output, such as performance, efficiency or validation accuracy. Because the function is high-dimensional and likely complex, global optimisation is hard, so identifying strong local maxima is often a practical strategy. For example, imagine you’re tuning an ML model with eight hyperparameters: learning rate, batch size, number of layers, dropout rate, regularisation strength, activation function (numerically encoded), optimiser type (encoded) and initial weight range. Each input set returns a single validation accuracy score between 0 and 1. Your goal is to maximise this score. |

## Section 2: Navigating this repository

## Section 3: Inputs and Outputs

Inputs: Eight sets of input query vectors of varying dimensions 2D to 8D (Functions 1 to 8) in a hyphen-separated format x1-x2-…-xn to 6 decimal places (e.g. 0.123456-0.789876 for 2D). Every component in each query vector must lie between 0 and 1. Limited budget (and limited data), one query per function per weekly submission.

Outputs: One single scalar performance value output (positive or negative) per query per input function.

## Section 4: Challenge Objectives

The objective of the BBO capstone project is to optimise a set of eight unknown functions using only limited, sequentially acquired data. Each function represents a maximisation problem, where the input values are used to produce the highest possible output. The optimisation must rely entirely on observed input–output pairs and intelligent search strategies.

Constraints: One submission query per function per week; response delay with outputs only revealed after each weekly submission cycle; variations in dimensionality (2D to 8D); noise levels; highly non-linear. This makes traditional analytical optimisation impossible.

## Section 5: Weekly Query Point Output Results Weeks 1 to 9

| Function | Best from initial data | Week 1 | Week 2 | Week 3 | Week 4 | Week 5 | Week 6 | Week 7 | Week 8 | Week 9 | Week 10 | Week 11 | Week 12 |
|----------|------------------------|--------|--------|--------|--------|--------|--------|--------|--------|--------|---------|---------|---------|
| F1 (2D)  | 
| F2 (2D)  | 
| F3 (2D)  |
| F4 (2D)  |
| F5 (2D)  |
| F6 (2D)  |
| F7 (2D)  |
| F8 (2D)  |

## Section 6: Technical Approach

### Weeks 1–3:

The approach has been deliberately exploration‑heavy, reflecting the limited data available and the risk of converging too quickly on suboptimal regions. Each function required slightly different handling depending on dimensionality, noise and structure. Week 1 began with conservative EI‑based exploration, Week 2 increased exploration using UCB, and Week 3 introduced more function‑specific heuristics and stronger uncertainty‑driven search.

### Week 4:

### Week 5:

### Week 6: 

### Week 7:

### Week 8: 

### Week 9:



### Week 10:

#### Overall Strategy (Week 10)
Week 10 marks the final exploitation phase of Bayesian Optimisation. Across all functions:
•	Expected Improvement (EI) uses very small ξ (0.0005–0.005) → near-greedy behaviour 
•	Search radii are tight (≈0.02–0.03) → local refinement only 
•	Gaussian Processes (GPs) are well-trained from Weeks 1–9 
•	Focus shifts from exploration → fine-tuning near best-known optima 

#### Function-by-Function Summary (Week 10)
##### Function 1 (2D, deterministic, sparse peaks)
•	Data mostly near zero with sharp, narrow peaks 
•	GP: RBF kernel, low noise (α=1e-6), log-transformed outputs 
•	Strategy: 
  o	Local EI optimisation (ξ=0.005) 
  o	Radius = 0.02 around best point 
•	Query: [0.629953, 0.486520] 
•	Insight: 
  o	Peaks are highly localised → pure exploitation 
  o	Goal: refine contamination source detection 

##### Function 2 (2D, noisy, multimodal)
•	Noisy outputs with multiple local maxima 
•	GP accounts for uncertainty (slightly higher α) 
•	Strategy: 
  o	EI (ξ=0.005), but noise-aware 
  o	Local search with multiple restarts 
•	Query: [0.533026, 0.565895] 
•	Insight: 
  o	Similar to Function 1, but more cautious 
  o	Noise can mislead optimisation → careful refinement 

##### Function 3 (3D, negative outputs transformed)
•	Objective: minimise side effects (via maximisation transform)
•	Outputs shifted + log-transformed for GP stability
•	GP: 
  o	RBF with short length-scale in dimension 3 (high sensitivity)     
•	Strategy:
    o	Tight bounds around best region    
    o	EI with ξ=0.005     
•	Query: [0.869309, 0.567474, 0.093237] 
•	Insight: 
    o	Strong dimension-specific sensitivity   
    o	Focused exploitation in promising drug combinations 

##### Function 4 (4D, multimodal hyperparameters)
•	Complex landscape with multiple local optima
•	GP trained on 37 points
•	Strategy:
    o	EI (ξ=0.003)    
    o	Tight bounds (±0.02)   
    o	Differential Evolution (DE) + jitter     
•	Query: [0.401766, 0.385109, 0.392801, 0.432944]
•	Insight:
    o	DE helps avoid local traps even in small regions   
    o	PCA confirms clustering near optimum 

##### Function 5 (4D, unimodal)
•	Clear single peak near [1,1,1,1] 
•	GP assumes near-deterministic behaviour (α≈0) 
•	Strategy: 
    o	Extremely small ξ = 0.0005     
    o	Ultra-tight bounds near optimum    
•	Query: [0.999992, 0.999997, 0.999996, 0.990008] 
•	Insight: 
  o	Pure exploitation 
  o	Fine-tuning at numerical precision level 

##### Function 6 (5D, structured, near-unimodal region)
•	ARD kernel identifies dimension sensitivities 
•	Best previous point refined locally 
•	Strategy: 
  o	EI (ξ=0.0005) 
  o	Bounds ±0.03 
•	Query: [0.374036, 0.285500, 0.745577, 0.848678, 0.130795] 
•	Insight: 
  o	Small shifts toward boundaries (x₁, x₅) 
  o	Exploits ingredient sensitivity learned by GP 

##### Function 7 (6D, hyperparameter tuning)
•	High-dimensional optimisation with GP + EI 
•	Strategy: 
  o	Very local search (radius = 0.02) 
  o	DE optimisation 
•	Query: [0.1482, 0.1625, 0.3973, 0.2662, 0.2852, 0.8291] 
•	Insight: 
  o	Likely near optimum → fine-tuning stage 
  o	Risk: search may be too local 
  o	Suggested improvement: slightly larger radius or multiple restarts 

##### Function 8 (8D, complex multimodal)
•	Most complex function; ARD reveals dimension importance 
  o	Key dims: 0, 2, 5, 6 
  o	Irrelevant dim: 7 (length-scale ~100) 
•	Strategy: 
  o	EI (ξ≈0.001) 
  o	Local refinement + boundary push 
•	Query: [0.0358, 0.0832, 0.1629, ~0, 0.7542, 0.4736, 0.1572, 0.8728] 
•	Insight: 
  o	Movement along a ridge toward boundary (dim 3 → 0) 
  o	GP very confident → EI nearly flat 
  o	Indicates near convergence 

#### Key Takeaways Across Functions
•	Exploitation dominates: minimal exploration remains 
•	EI is nearly flat → only small improvements possible 
•	ARD kernels guide dimension-wise focus 
•	Boundary behaviour becomes important in high dimensions 
•	Transformations (log, shifting) improve GP stability 
•	Differential Evolution + restarts ensure robustness 

#### Conclusion
Week 10 represents late-stage convergence:
•	All functions show tight clustering around optima 
•	Improvements are incremental and diminishing 
•	Strategy is consistent: trust the GP and refine locally 
The optimisation process is now preparing for final confirmation (Weeks 11–12) rather than discovery.

### Week 11



### Week 12
