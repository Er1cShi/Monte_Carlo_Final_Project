# Monte Carlo Final Project

Adaptive Sample Allocation in Multilevel Monte Carlo for Option Pricing

## Overview

This project studies Monte Carlo (MC) and Multilevel Monte Carlo (MLMC) methods for option pricing. It starts from the Black-Scholes setting, reproduces core ideas from Michael B. Giles' MLMC path simulation paper, and then introduces a modified iterative variance-stabilized MLMC allocation rule.

The main research question is:

> Can an adaptive sample allocation strategy improve the practical efficiency of MLMC for option pricing compared with the original Giles allocation rule?

## Project Structure

```text
.
├── code/
│   └── MC_final_Project.ipynb
├── docs/
│   ├── MLMC_Giles.pdf
│   ├── MLMC_Giles.txt
│   ├── mc_project_proposal.pdf
│   └── mc_project_proposal.txt
└── README.md
```

## Main Components

The notebook in `code/MC_final_Project.ipynb` contains:

1. **Black-Scholes and Standard Monte Carlo**
   - Black-Scholes closed-form European call benchmark
   - Standard Monte Carlo European call pricing

2. **Baseline MLMC**
   - Coupled fine/coarse Brownian paths
   - European, Asian, and barrier payoff examples
   - Fixed-allocation MLMC prototype

3. **Giles MLMC Reproduction**
   - Geometric Brownian motion with Giles' parameters:
     - `S0 = 1`
     - `K = 1`
     - `r = 0.05`
     - `sigma = 0.2`
     - `T = 1`
     - `M = 4`
   - Euler discretization
   - European and arithmetic Asian call payoffs
   - Original Giles adaptive sample allocation

4. **Modified MLMC**
   - Iterative variance-stabilized allocation
   - Damped and capped sample updates
   - Allocation stabilization checks

5. **Final Evaluation Framework**
   - Fair reference prices
   - Standard MC for European and Asian options
   - Runtime tracking
   - Repeated-run RMSE
   - Cost, runtime, and efficiency comparisons
   - Ratio-based metrics:
     - `RMSE_Ratio`
     - `Cost_Ratio`
     - `Runtime_Ratio`
     - `Efficiency = 1 / (RMSE^2 * Cost)`

## Methods Compared

- Standard Monte Carlo
- Original Giles MLMC
- Modified iterative variance-stabilized MLMC

## Evaluation Metrics

The project compares methods using:

- Option price estimate
- Standard error
- RMSE
- Runtime
- Total computational cost
- Level-by-level sample allocation
- RMSE ratio between modified and original MLMC
- Cost ratio between modified and original MLMC
- Runtime ratio between modified and original MLMC
- Efficiency ratio between modified and original MLMC

## How to Run

Open the notebook:

```text
code/MC_final_Project.ipynb
```

Recommended execution order:

1. Run the setup and baseline MC cells.
2. Run the Giles MLMC definition cells.
3. Run the modified MLMC definition cells.
4. Run the final experiment framework.
5. Run the ratio-based evaluation cells.

For faster development runs, use the smaller test settings in the notebook:

```python
FINAL_TEST_EPSILONS = [1e-3, 5e-4]
FINAL_TEST_REPS = 3
```

For final report-quality results, increase the number of repetitions and use the full Giles epsilon list:

```python
GILES_EPSILONS = [5e-5, 1e-4, 2e-4, 5e-4, 1e-3]
```

## References

- Giles, M. B. (2008). *Multilevel Monte Carlo Path Simulation*. Operations Research, 56(3), 607-617.
- Higham, D. J. (2015). *An Introduction to Multilevel Monte Carlo for Option Valuation*. International Journal of Computer Mathematics.

