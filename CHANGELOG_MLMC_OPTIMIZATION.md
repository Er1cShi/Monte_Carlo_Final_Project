# MLMC Notebook Optimization Notes

This note summarizes the latest updates to `code/MC_final_Project.ipynb`.

## What Changed

- Added batch/vectorized sampling for Giles MLMC level samples.
- Kept Original Giles MLMC and Modified MLMC on the same sampling backend.
- Aligned comparison sample settings with Giles-style initial sampling through `GILES_INITIAL_SAMPLES`.
- Reduced `FINAL_REPS` to `3` to make the full comparison more practical to run locally.
- Added automatic output saving under `output/`.
- Added `output/.gitkeep` so the output folder is visible in the repository.

## Why This Was Changed

The previous notebook generated MLMC level samples one path at a time in Python. That made the full Giles-consistent comparison very slow, especially for small epsilon values. The new batch sampler generates many paths at once using NumPy arrays, reducing Python loop overhead while preserving the same MLMC estimator and fine/coarse Brownian coupling.

## Effect on Giles Reproduction

The mathematical experiment is unchanged:

- Same GBM parameters: `S0=1`, `K=1`, `r=0.05`, `sigma=0.2`, `T=1`.
- Same Euler discretization.
- Same refinement factor `M=4`.
- Same coupled fine/coarse Brownian increments.
- Same Giles allocation rule.
- Same Giles bias stopping rule.

Only the implementation of sample generation was changed from per-path loops to batched computation.

## Effect on Modified MLMC

The modified method is still the same allocation experiment:

- It uses the same estimator as Giles MLMC.
- It uses the same payoff definitions and Brownian coupling.
- It still updates sample allocation iteratively with damping and caps.
- It now benefits from the same faster batch sampler used by the original Giles method.

This keeps the comparison fair because both methods use the same optimized sampling backend.

## Output Files

After running the final experiment cells, the notebook writes results to `output/`:

- `final_comparison_rows.csv`
- `final_summary_rmse_cost_runtime.csv`
- `reference_prices.csv`
- `final_comparison_plots.png`
- `sample_allocation_european.png`
- `sample_allocation_asian.png`
- `mlmc_modified_vs_original_ratios.csv`
- `mlmc_ratio_metrics.png`

If `pandas` is unavailable, table outputs fall back to JSON files.

## Runtime Note

Even with batching, the full Giles epsilon list can still be expensive because sample counts scale roughly like `epsilon^-2`. For quick checks, run fewer epsilon values first. For report-quality results, use the full `GILES_EPSILONS` list.
