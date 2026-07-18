# Methods Revision: Peak-relative Windows, Tau, and Cis Evidence

## Peak-relative activation windows

Family-level `sum_` expression was fitted on a common 1,001-point `dev01` grid using the existing cubic B-spline GAM-style workflow. Fitted log2(expression + 1) values were returned to linear scale. For each trajectory, the fifth percentile was used as baseline and the fitted dynamic range was normalized to 0-1. The main threshold was q=0.25, with q=0.10 and q=0.50 retained for sensitivity analysis. Contiguous above-threshold components were identified separately; the primary component contained the global peak. Onset and shutdown were linearly interpolated threshold crossings. Activation T50 was the time at which 50% of cumulative fitted activation above q occurred within the primary component. Boundary-contacting windows were marked as censored, and secondary components with at least 25% of the primary area were marked multimodal.

## Tau specificity

Tau was calculated from non-negative linear-scale expression as sum(1 - x/max(x))/(n - 1). Tau=0 denotes broad expression and Tau=1 denotes restricted expression. Temporal Tau used each organ-specific fitted trajectory on the common dense grid. Organ Tau used the maximum fitted expression for each observed organ; missing organs were not replaced with zero. Fig.3g used one independent ERV-family row: Tau was summarized by the median across species, recurrent families had dynamic calls in at least three species, lineage-biased families had dynamic calls in one or two species, and families without any dynamic call were excluded. Fig.3e and Fig.4e retained one species-family row because their driver and cis-support labels are species-specific. Median differences, 95% bootstrap confidence intervals, two-sided Mann-Whitney tests, Benjamini-Hochberg FDR and Cliff's delta were reported.

## Cis evidence

Significant cis pairs, driver-versus-background odds ratios and confidence intervals were taken from the archived formal all-species driver follow-up tables. Positive target genes were deduplicated within family-species strata. Example trajectories were drawn only when both the ERV locus matrix and transcript-to-gene mapping supported the pair. Cis association was interpreted as coupling, not causality. GO/KEGG/pathway enrichment was not presented because the formal source tables were unavailable and no complete tested-gene-universe enrichment provenance was present.
