Experiment Tracker

This table records all modelling experiments, including data slices, models, metrics and decisions. Each experiment ID should be unique and referenced in the decisions log.

| Date | Experiment ID | Purpose | Data slice | Model | Metrics (AUROC/AUPRC, calibration) | Subgroup metrics (TPR/FNR differences) | Result | Decision | Next step |
|---|---|---|---|---|---|---|---|---|---|


Metric Glossary

AUROC (Area under the Receiver Operating Characteristic curve) – measures discrimination across thresholds; values closer to 1 indicate better ranking.

AUPRC (Area under the Precision–Recall curve) – useful for imbalanced datasets; higher values indicate better precision and recall across thresholds.

Calibration slope/intercept – assesses agreement between predicted probabilities and observed outcomes; ideal slope = 1 and intercept = 0.

TPR (True Positive Rate) – proportion of monogenic cases correctly classified; also called sensitivity.

FNR (False Negative Rate) – proportion of monogenic cases incorrectly classified as unexplained (1 − TPR).

Disparity measures – differences in TPR or FNR across protected groups (sex, ethnicity, age, deprivation). A value of 0 indicates perfect parity. Ratios (e.g. TPR_groupA/TPR_groupB) may also be reported.
