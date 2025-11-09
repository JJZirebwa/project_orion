Governance Card – ICD-10 Brugada Classification

This governance card documents the intended use, assumptions, risks and controls for the machine-learning model developed in Project ORION v2. It reflects requirements for responsible AI and follows SaMD-like documentation suggested in the project discussion.

Intended Use & Users

Purpose – To classify Brugada syndrome patients into monogenic (likely pathogenic variant in SCN5A or related genes) or unexplained groups based solely on ICD-10 codes from hospital episode statistics. This classifier acts as a triage tool to prioritise patients for genetic testing and research, not as a standalone diagnostic.

User groups – Researchers and clinicians within the Genomics England TRE; project supervisor Dr Tim Hearn; academic assessors. No direct clinical deployment is intended during the project timeline.

Context of use – Analyses are performed within a Trusted Research Environment (National Genomics Research Library), using de-identified data. Outputs may inform research papers or recommendations but must not be used for patient care without further validation and regulatory approval.

Inputs / Outputs

Inputs –

ICD-10 codes from hospital episode statistics per patient. Codes are aggregated into feature vectors using counts, temporal patterns and comorbidity indices (Working Theory). Codes occurring after the genetic diagnosis will be excluded to avoid leakage.

Demographic attributes (sex, age at recruitment, ethnicity, deprivation index) used for fairness analysis and optional model features.

Genetic label – binary indicator of monogenic Brugada (variants in SCN5A) versus unexplained, derived from genomic sequencing data【project_description.docx】.

Outputs –

Predicted probability that a patient belongs to the monogenic group.

Binary classification (monogenic/unexplained) based on a chosen threshold.

Subgroup metrics summarising performance across protected attributes.

Assumptions & Exclusions

Assumes accurate linkage between ICD-10 codes and genetic labels; HES coding captures clinically relevant history and is unbiased by referral【project_description.docx】.

Assumes patient episodes prior to genetic testing reflect disease burden and are representative of the diagnostic odyssey.

Excludes unstructured text, HPO terms, laboratory values or imaging (not available in current scope). Use of patient letters or promoter-variant classification is explicitly out of scope【project_description.docx】.

Assumes no direct patient involvement; any survey work would require separate ethics under supervisor’s existing approvals【project_description.docx】.

Model Classes Under Consideration

| Class | Rationale | Notes |
|---|---|---|
| Logistic / Generalised linear models | Provide interpretable baseline and calibrate well; baseline suggested by supervisor. | Use regularisation to handle high-dimensional codes. |
| Random forest | Previously explored by the research team【project_description.docx】; handles non-linear relationships and interactions. | Evaluate variable importance for feature insights. |
| Shallow neural network | Step towards deep learning; can model complex code embeddings with modest computational cost【project_description.docx】. | Use dropout and regularisation to prevent overfitting. |
| Deep sequence models (Working Theory) | Only if time permits; may model temporal sequences of ICD-10 codes. | Requires careful tuning; flagged as optional. |

Error Types & Harm Scenarios

| Error type | Potential harm | Mitigation |
|---|---|---|
| False positive (unexplained misclassified as monogenic) | May prioritise patients unnecessarily for genetic testing, consuming resources and raising expectations. | Use conservative thresholds; provide probability scores; monitor referral burden. |
| False negative (monogenic misclassified as unexplained) | Patient might not receive timely genetic testing, perpetuating diagnostic delays. | Optimise for recall; incorporate human oversight; emphasise that model is adjunct, not replacement. |
| Systemic bias | Disparities across sex, ethnicity, age or deprivation indices could worsen inequities. | Perform subgroup analysis; adjust thresholds or reweight; audit features for proxies. |
| Model drift | Changes in coding practices or patient mix could degrade performance. | Monitor performance periodically; retrain with updated data. |
| Misinterpretation by users | Users may over-interpret probabilities as definitive diagnoses. | Provide clear documentation and training; emphasise limitations. |

Subgroup Performance Plan

1. Protected attributes – Analyse performance by sex (male/female), age group (e.g. <40, 40–60, >60), ethnicity categories (e.g. White, Black, Asian, Mixed/Other) and deprivation quintiles.

2. Fairness metrics – Report true-positive-rate (TPR) and false-negative-rate (FNR) per subgroup; compute differences and ratios. Measure calibration error across groups. Use equalised odds and demographic parity difference as secondary metrics (Working Theory).

3. Mitigation options – If disparity > 10 percentage points, consider threshold adjustment by subgroup, sample reweighting, or re-training with fairness-aware algorithms. Document the effect on overall performance and equity plan.

4. Reporting – Include subgroup tables in experiment tracker; discuss results in dissertation; review with supervisor before final submission.

Risk Controls

Data governance – Strictly comply with Genomics England TRE policies and information-governance training.

Documentation & reproducibility – Maintain a version-controlled codebase; log dataset versions, feature transformations and random seeds; ensure analyses can be reproduced within the TRE. Record decisions in decisions.md.

Code review & supervision – Schedule periodic reviews with the supervisor or PhD collaborator; record outcomes in the experiment tracker and decisions log.

Ethics & regulatory review – Confirm that existing ethics approvals cover the study; if any patient contact occurs, use supervisor’s umbrella ethics and document accordingly【project_description.docx】.

Sign-off points – Before finalising models, obtain supervisor sign-off on: feature set definition; model choice; fairness evaluation; and presentation content.

Data-integrity controls: assert preserved patient counts per split; forbid post-diagnosis features; enforce date windows; monitor missingness deltas; verify label derivation; ensure split purity (no patient overlap). Training is blocked if any control fails. All processing remains in TRE; only aggregates/plots leave under disclosure control.


Service Impact View (Template)

For every 100 patients referred for Brugada genetic testing:

Without model – All 100 receive genetic testing; monogenic yield is Y % (to be derived from data).

With model – The classifier prioritises P patients (top probability decile) for immediate testing, capturing Q % of monogenic cases. R patients are deprioritised; their testing may be deferred.

Subgroup differences – Report how P, Q and false-negative counts vary across subgroups. Comment on potential benefits or harms to each group.

Actual numbers will be populated once data analysis is complete. This framing provides a simple, per-100-patients narrative for clinicians and policymakers.

Regulatory & Policy Hooks

Data protection – Comply with the UK General Data Protection Regulation (GDPR) and Data Protection Act 2018; work only with de-identified data within the TRE.

Ethics approvals – Use existing hospital ethics for secondary analyses; document any patient-survey component under the supervisor’s ethics【project_description.docx】.

Software-as-a-Medical-Device (SaMD) – Recognise that any future clinical deployment would be regulated by the UK Medicines and Healthcare products Regulatory Agency (MHRA); follow best practices in model documentation, performance reporting and risk management.【project_description.docx】

Academic integrity – Adhere to ARU policies on plagiarism, academic honesty and reporting. All sources and code must be properly attributed.

Brugada syndrome should be referenced as ICD-10 I49.8 (‘Other specified cardiac arrhythmias’). This is a broad bucket; treat it as a feature rather than a gold-standard label. For ICD-11, use BC65.1 for mapping.
