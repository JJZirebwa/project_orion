Decisions Log

Project decisions are recorded in RFC-style entries. Each entry should cite relevant sources and be revisited on the specified review date.

Decision 1: Label Definition for Brugada Cohort

Context – The project aims to classify Brugada syndrome patients into monogenic versus unexplained groups using ICD-10 codes. The genetic label must be defined consistently.

Options

Use SCN5A pathogenic/likely pathogenic variants as the sole definition of “monogenic” and classify all others as “unexplained”.

Include variants in additional Brugada-associated genes (e.g. SCN10A, CACNA1C) if evidence emerges.

Use clinical phenotype or HPO terms to define labels (contrary to the project’s core premise【project_description.docx】).

Decision – Option 1 is adopted as the primary label definition. Only patients with pathogenic or likely pathogenic variants in SCN5A are labelled as monogenic; others are unexplained.

Rationale – The supervisor’s description focuses on SCN5A monogenic cases and unexplained patients【project_description.docx】. Expanding to additional genes would complicate the analysis and may require re-curation of variant interpretations. Using phenotype-based labels contradicts the goal of predicting genetics from ICD-10 codes.

Consequences – Simplifies label curation and allows clear binary classification. May underestimate the true monogenic cohort if other genes contribute; future work could extend the definition. Requires careful handling of variant annotation to avoid mislabelling.

Review date – Week 6; revisit if new genetic evidence or supervisor advice warrants expansion.

Decision 2: Baseline Model Selection

Context – The supervisor suggested random forest and neural network models. JJ proposed including a logistic regression baseline. The choice of baseline influences evaluation and interpretability.

Options

Start with logistic regression (with regularisation) as the primary baseline and compare against random forest and shallow neural network.

Begin directly with random forest and neural network, omitting simpler models.

Explore only deep learning approaches.

Decision – Option 1 is adopted. Implement a generalised linear/logistic model as the baseline, followed by random forest and a shallow neural network.

Rationale – A logistic model provides an interpretable benchmark and helps calibrate expectations; it can highlight whether more complex methods are warranted. Supervisor recommended random forest and neural network, so they will be evaluated after establishing a baseline. Exclusively deep learning (Option 3) is risky given time and skill constraints.

Consequences – Additional coding effort to implement multiple models, but yields a richer comparison. If performance difference between logistic and complex models is minimal, adoption of simpler model may be justified. Need to ensure fairness analysis is conducted for each model.

Review date – After Experiment 3 (expected Week 9) when all three models have been evaluated.

Decision 3: Dataset Split Strategy

Context – Proper separation of training and test data is critical to avoid information leakage. Hospital episode data are longitudinal and may include episodes occurring after genetic diagnosis.

Options

Patient-level random split (e.g. 70/15/15) without regard to time.

Temporal split: use episodes before a cutoff date for training and later episodes for testing.

Hybrid split: patient-level split with censoring of post-diagnosis codes.

Decision – Option 3 is adopted. Patients are randomly assigned to training, validation and test sets, but episode data are censored so that only codes occurring prior to genetic diagnosis are used for feature construction; codes after diagnosis are excluded from all sets.

Rationale – Patient-level split prevents data leakage across sets, and censoring codes after diagnosis reduces risk of using outcome information as input. A purely temporal split (Option 2) may leave insufficient test cases if diagnosis dates vary widely. Random split without censoring (Option 1) risks leakage and inflated performance.

Consequences – Requires accurate diagnosis dates; may reduce feature richness for some patients. Should document any removed codes. Performance estimates will reflect pre-diagnosis prediction use case.

Review date – Week 5; adjust if data exploration reveals different episode distributions or supervisor advises otherwise.


| Date | ID | Category | Decision | Rationale (short) | Status | Follow-ups |
|---|---|---|---|---|---|---|
| 2025-10-06 | DEC-ICD10-0001 | Coding standard | Use ICD-10 I49.8 for Brugada (not I47.2). Treat I49.8 as feature; note ICD-11 BC65.1. | I49.8 explicitly includes Brugada; I47.2 is ventricular tachycardia. I49.8 is broad → not a label. | Accepted | Update ontology_map.md, data_audit_checklist.md; add QA check in next release. |
| 2025-10-21 | DEC-PROCESS-0002 | Process | Treat dissertation as method-development + evaluation; document every iteration (methods, code variants, results). | Aligns with Biomedical marking; shows method, not just end product. | Accepted | Reflect in charter & appendices structure. |
| 2025-10-21 | DEC-INTEGRITY-0003 | Data integrity | Enforce TRE-grade integrity tests; block training if any test fails. | Demonstrates patient-data integrity; prevents leakage. | Accepted | Add tests to data_audit_checklist.md; reference in governance_card.md. |
| 2025-10-21 | DEC-STREAMS-0004 | Process | Run two streams in parallel: method-development and data-analysis; link them in write-up even if final integration is partial. | Preserves progress if one stream lags; matches supervisor advice. | Accepted | Note in supervision_pack_template.md “Process + Analysis Streams”. |
| 2025-10-21 | DEC-PLANNING-0005 | Planning | **Supersede all preliminary sprints/plans** until TRE training transcript is mined and the Agent outputs a new execution plan. | Avoids drift from outdated assumptions. | Accepted | Remove old sprint rows; clear placeholder experiment rows. |


