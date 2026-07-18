# Methods: native-age GAM, post-hoc alignment, Tau, and residual cis recurrence

## Developmental trajectory modelling and alignment

For each species, organ and annotated ERV family, sample-level family-summed TPM was transformed as log2(TPM + 1) and modelled as a smooth function of log1p(days post conception). Dynamic calls were made on the native-age model using the pre-specified sample, stage, FDR and amplitude filters. Prediction was restricted to the observed native-age range.

The native-age fitted curves were subsequently mapped, without refitting, to a mouse-reference developmental maturity coordinate. The mapping used the published host-transcriptome stage correspondence with mouse stages E10.5, E11.5, E12.5, E13.5, E14.5, E15.5, E16.5, E17.5, E18.5, P0, P3, P14, P28 and P63 indexed from 0 to 13. For source stages mapped to more than one mouse stage, lower, midpoint and upper indices were retained; midpoint was primary. Monotone piecewise-linear interpolation was used between anchors, and no trajectory was extrapolated beyond anchor support.

## Activation episodes and uncertainty

Fitted values were back-transformed to the TPM response scale. For each curve, the fifth percentile was used as a robust baseline and activation was normalized by the difference between the fitted maximum and baseline. At q = 0.25, contiguous components above q were identified. The component containing the global fitted maximum was the dominant activation episode; separated components were never bridged. Onset and shutdown were linearly interpolated threshold crossings. Activation T50 was the time at which 50% of the area above q accumulated within the dominant episode. Components touching the mapped support boundaries were marked left- or right-censored. A trajectory was marked multimodal when a secondary component had at least 25% of the primary component area.

Sensitivity analyses used q = 0.10 and q = 0.50 and lower/upper alignment anchors. Biological samples were resampled with replacement within species-organ-stage strata for 1,000 formal bootstrap iterations; single-sample stages were held fixed. Dominant components were tracked against the original interval, and reproduction below 80% was marked unstable.

## Tau specificity

Temporal Tau was computed from non-negative response-scale fitted values at the fixed mouse-reference stages that fell within observed mapped support, requiring at least five stages. Organ Tau was computed across eligible organs using each organ's maximum response-scale fitted expression. Missing organs were not treated as zero. Tau was defined as sum(1 - x_i/max(x))/(n - 1), where 0 denotes broad expression and 1 denotes restricted expression.

For the main recurrence analysis, one independent annotated ERV family contributed one point. Species-level temporal Tau was the median across valid dynamic organs, and species-level organ Tau used all eligible organs. Family values were the medians across dynamic species. Families dynamic in at least three species were recurrent, those dynamic in one or two species were lineage-limited, and those dynamic in no species were unclassified. Group differences used exact family-label permutation, Cliff's delta and family-level bootstrap confidence intervals, with BH correction across temporal and organ Tau.

## Driver sensitivity

The core driver score remained independent of Tau and cis evidence: max(0, Spearman correlation between a locus trajectory and its family mean trajectory) multiplied by locus mean TPM. A leave-one-out sensitivity analysis recalculated the family reference after excluding the focal locus. Score-rank correlation and top-decile overlap were reported by species and organ.

## Residual cis coupling and cross-species recurrence

Transcript-to-gene aggregation used the actual species-specific Ensembl transcript-gene mapping tables rather than identifier-prefix substitution. For each eligible ERV-gene pair, ERV and gene log2(TPM + 1) were separately residualized against smooth nonlinear log1p(days post conception) and sex. Spearman correlation between residuals was used as the primary age-independent coupling statistic. BH correction was applied within species-organ strata; significant residual associations required |rho| >= 0.30 and FDR < 0.05. Total developmental coexpression and the legacy partial-Spearman result were retained only as supplementary comparators.

Target-gene recurrence used Ensembl Compara release 112 protein homologies and prioritized orthogroups with a unique gene per species. Evidence was filtered sequentially by the same annotated ERV family-target orthogroup in at least two species, exact organ agreement, ERV activation-T50 difference of at most one matched stage, and effect-direction agreement. Window IoU >= 0.5 was retained as sensitivity evidence.

For module-level convergence, one-to-one host-gene orthogroups represented in at least four species were aligned to fixed reference stages and z-standardized within species. A consensus profile was retained when at least four species contributed at a stage; orthogroup-organ profiles required at least five common stages. Average-linkage clustering used 1 - Pearson correlation, cut height 0.30 and minimum module size five. Module recurrence was evaluated only for significant positive residual cis targets and was interpreted as functional convergence rather than exact target conservation.
