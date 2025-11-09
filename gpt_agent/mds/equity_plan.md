Purpose & scope

Ensure the model’s predictions are well-calibrated and comparably accurate across key subgroups relevant to Brugada work-ups, and document any disparities with clear mitigation steps. This is a research evaluation (not deployment).

Subgroups (fill from your data dictionary)

Sex: {female, male, other/unknown*}

Ethnicity: {dataset categories as recorded; include “unknown” as its own level}

Deprivation: national deprivation quintiles (Q1 least deprived → Q5 most deprived)

*Unknown/missing must be treated as explicit categories to avoid silent exclusion.

Datasets & sufficiency

Splits: patient-level train / validation / test. Integrity checks must pass before any fairness analysis.

Minimum n per subgroup on test: at least 50 positives and 50 negatives, or report metrics with caution and prioritise AUROC/CIs over thresholded rates for small cells.

Operating point policy (threshold selection)

Set a single operating threshold on the validation set (record method and value).

Apply that threshold unchanged to the test set and all subgroups.

Default policy (research): Youden’s J on validation. Alternative (if agreed): target PPV chosen with the clinical team. Record the choice in thresholds_policy.md.

Metrics

Overall (test set)

AUROC, AUPRC (with 95% bootstrap CIs, resample by patient)

Brier score; Calibration slope & intercept; ECE (10–20 equal-width bins)

Subgroup fairness (test set, at fixed threshold)

ΔTPR and ΔFNR per subgroup family (max − min across levels)

ΔPPV per subgroup family

ECE per subgroup (calibration-in-the-small)

Alert thresholds (research defaults, adjustable)

Flag for review if any condition holds:

|ΔTPR| > 0.05 or |ΔFNR| > 0.05 (within a subgroup family)

|ΔPPV| > 0.07 (within a subgroup family)

Subgroup ECE difference > 0.02 (max − min)

These are review triggers, not automatic “fail” states. Discuss clinical relevance and sample size.

Mitigation playbook (choose minimally invasive first)

Data/feature audit: remove obvious proxy features; confirm pre-diagnosis censoring.

Re-calibration: pooled isotonic/Platt; if needed, report subgroup calibration, but avoid per-subgroup calibrators unless justified.

Re-weighting / class balance: instance weights or class_weight to reduce subgroup loss imbalance.

Threshold audit: explore subgroup-specific thresholds for analysis only; report outcomes and ethical trade-offs; keep single threshold as primary.

Model choice/regularisation tweak: e.g., adjust RF depth/leaves; try simpler models if variance drives disparity.

Sensitivity analyses: rerun with alternative feature sets / windows to test robustness of gaps.

Reporting requirements (for dissertation & model card)

Table A (overall): AUROC, AUPRC, Brier, slope, intercept, ECE (+ 95% CIs).

Table B (subgroups): per-level TPR/FNR/PPV, with Δ summary per family (+ CIs if stable).

Figure: calibration curve (overall) + small-multiples by subgroup (optional if n allows).

Narrative: threshold method, any alerts triggered, mitigations attempted, net effect on service-impact (“per 100 patients”).

Provenance: split hash IDs; bootstrap settings; code/commit IDs.

Governance & change control

Any change to subgroup definitions, thresholds, or mitigation approach → add an entry in decisions.md and bump Equity Plan version here (see header).

All analyses remain inside the TRE; only aggregate tables/figures leave under disclosure rules.

Version

Equity Plan v1.0 — 2025-10-21 (initial research defaults; thresholds adjustable after supervisor review)