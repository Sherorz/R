# Fig.2-Fig.5 V2 Revision Report

Run date: 2026-07-17.

This revision is isolated under `/Users/lvtingwei/Desktop/项目/ERV_development/未命名文件夹/results/main_figures_revised_v2_20260716`. The legacy result tree was not used as an output destination.

## Main changes

- Fig.2d now uses peak-relative q=0.25 activation episodes and activation AUC-T50; no interval bridges separate components.
- Fig.3 and Fig.4 use linear-scale Tau with the explicit direction 0=broad and 1=restricted.
- Fig.5 is centered on cis evidence. Unsupported pathway labels were removed from main panels.
- Every panel has SVG, PDF and 600-dpi PNG output with a matching source-data table.

## Key results

- q=0.25 median window width: 0.324 dev01.
- q=0.25 left-censored: 52.7%; right-censored: 23.2%; multimodal: 17.5%.
- Fig.3g uses independent families: 16 recurrent and 3 lineage-biased; families without dynamic calls are excluded.
- Lineage-biased families show higher temporal Tau (median difference=0.140, FDR=0.00454) and organ Tau (median difference=0.162, FDR=0.0119) than recurrent families.
- Driver and cis-supported driver families show lower Tau, consistent with broader or moderately broad expression rather than universal high specificity.
- Valid formal pathway-enrichment rows available for the main figure: 0.

## Verification

- Unit and contract tests: 58 passed.
- Configuration readiness: 79 PASS, 0 BLOCKED, 0 FAIL.
- Python compilation: passed.
- Panel artifacts: 66 files (22 panels x SVG/PDF/PNG), 0 missing or empty.
- Assembled artifacts: 12 files (4 figures x SVG/PDF/PNG), 0 missing or empty.
- Fig.3g panel and assembled Fig.3 were inspected at original render resolution.

## Limitations

- Peak-relative windows are descriptive fitted episodes and boundary-censored trajectories do not have fully observed biological onset or shutdown.
- Most species×organ cis odds ratios are imprecise and do not pass FDR<0.05; the forest plot emphasizes effect size and uncertainty.
- Several species' current gene TPM files are not transcript-level, so example ERV-gene trajectories are restricted to pairs that pass identifier mapping QC.
- The lineage-biased group in Fig.3g contains only 3 independent families, so its effect size and uncertainty should be emphasized over asymptotic P values.
- Cis correlation does not establish causal regulation.
