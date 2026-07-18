# Aligned developmental analysis v3: run summary

## Output isolation

- New result root: `/Users/lvtingwei/Desktop/项目/ERV_development/未命名文件夹/results/main_figures_aligned_v3_20260717`
- Protected legacy result: `未命名文件夹/results/main_figures_revised_v2_20260716`
- Legacy files were read as inputs or sensitivity references only; no legacy result was overwritten.

## Core analysis

- Biological samples: 1675
- Annotated family labels: 20
- Native-age GAM groups fitted: 733
- Dynamic species-organ-family groups: 295 (legacy dev01 run: 349)
- Primary q=0.25 activation windows: 295
- Independent families in Fig.3 recurrence analysis: 15 recurrent and 3 lineage-limited.

## Fig.2 findings

- Native-age GAMs were fit before alignment; fitted curves were mapped post hoc to the mouse-reference host-transcriptome coordinate.
- q=0.10 versus q=0.25: T50 rho=0.992, median absolute shift=0.195 stages, class concordance=73.9%, interval IoU=0.902.
- q=0.50 versus q=0.25: T50 rho=0.993, median absolute shift=0.251 stages, class concordance=71.5%, interval IoU=0.762.
- Overall left-censored: 199/295 (67.5%).
- Overall right-censored: 81/295 (27.5%).
- Overall multimodal: 19/295 (6.4%).
- Formal biological-sample bootstrap: 1,000 iterations for 295 trajectories; 5 windows had component reproduction below 0.80.
- Median bootstrap T50 95% CI width: 1.372 matched stages.
- Family-clustered early-minus-late window-width difference: 6.904 [5.964, 7.300].
- Family-clustered early-minus-late temporal-Tau difference: -0.038 [-0.076, 0.005].

Interpretation: activation timing ranks are robust to q, but hard timing-class labels are only moderately stable. The aligned results support ordered and overlapping dominant activation episodes, not universally sharp discrete windows.

## Fig.3 findings

- Temporal Tau, lineage-limited minus recurrent: delta=0.037, exact P=0.25, FDR=0.25, Cliff delta=0.378.
- Organ Tau, lineage-limited minus recurrent: delta=0.243, exact P=0.0098, FDR=0.0196, Cliff delta=0.911.

Interpretation: the independent-family analysis supports greater organ restriction in lineage-limited families. Temporal restriction has the same direction but is not significant. The lineage-limited group contains only three families, so effect sizes and exact inference are emphasized.

## Driver sensitivity

- Core score remained `max(0, locus-family trajectory Spearman) x mean TPM`; Tau and cis were not added.
- Leave-one-out family-reference sensitivity: median score-rank rho=0.997; median top-10% overlap=98.6%; minimum evaluable fraction=97.0%.

Interpretation: including the focal locus in the historical family mean had little effect on ranking, but the leave-one-out results are retained as the formal sensitivity analysis.

## Fig.5 findings

- Residual cis eligible pairs: 92189; significant residual pairs: 4153.
- Orthologous family-target recurrence: 3 candidates.
- Same exact organ: 1; T50 matched within one reference stage: 1; direction-consistent: 1.
- Consensus-module gate passed in 7/7 organs.
- Positive residual cis module-level recurrences in at least two species: 91 family-organ-module units.

Interpretation: residual cis support is abundant at the pair level, but exact cross-species recurrence becomes sparse after orthology, organ, developmental-window and direction filters. Module-level convergence is broader and is presented as functional convergence, not exact conserved target regulation.

## Remaining limitations

- The original stage-alignment source table was unavailable. Global anchors were manually transcribed from the published Fig.2 correspondence and audited with lower/midpoint/upper one-to-many anchors.
- Published organ-specific and meiosis-adjusted anchor tables were not available, so early opossum heart, early human/rabbit ovary and gonadal meiosis sensitivity analyses remain blocked rather than approximated.
- The host-gene consensus modules are deterministic exploratory modules from aligned bulk-expression profiles; they are not a substitute for cell-type-resolved or experimental regulatory validation.
- Residual ERV-gene association does not establish causality.
