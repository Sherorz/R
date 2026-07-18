# ERV manuscript storyline V4 run summary

Run: `run_20260718_015200`

## Completed

- Canonical data layer, nomenclature audit and V1/V2/V3 crosswalk.
- 33 independent main-figure panels and 37 independent supplementary panels, each with TSV/PNG/PDF.
- Six assembled main figures and thirteen assembled supplementary figures, each in PNG/PDF.
- Thirteen supplementary tables, including the panel source-data index.
- Final 10,000-permutation module null, panel isolation test, statistical QA and visual QA.

## Frozen anchors

- 1,675 samples; 733 V3 GAM groups; 295 dynamic trajectories.
- 92,189 eligible residual cis pairs; 4,153 significant residual cis pairs.
- Three recurrent orthologous targets; one same-organ recurrence.
- 26,239 top-decile candidate loci under the independent activity score.

## Formal result changes

- Module convergence is not significant after 10,000 permutations (global empirical P = 0.4825); no unit is eligible for an affirmative main-figure claim.
- Matched-background cis OR is retained only as exploratory because the full planned matching covariates are absent.
- The stage-aligned storyline remains provisional until an official machine-readable correspondence table is verified.

## Explicit blockers

- FigS12 cell-composition sensitivity.
- Formal locus mappability adjustment.
- Derivative simultaneous confidence intervals.
- Sample-level candidate bootstrap and detectability-adjusted recurrence null.

## Re-render commands

```bash
Rscript code/R/render_v4.R code . panel Fig2c
Rscript code/R/render_v4.R code . figure Fig2
```
