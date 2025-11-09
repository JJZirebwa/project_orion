"Final-Year Project Charter – Project ORION v2
Mission & Problem Statement

Rare-disease patients often endure a “diagnostic odyssey”: approximately 70 % remain undiagnosed. The 100,000 Genomes Project recruited participants using disease and Human Phenotype Ontology terms, but this phenotype-only approach suffers from incomplete clinician-reported data. This project uses routinely collected International Classification of Diseases (ICD-10) codes from hospital episode statistics to classify Brugada syndrome patients into monogenic (e.g. SCN5A variants) or unexplained groups. The aim is to build a reproducible machine-learning pipeline within the National Genomics Research Library (a Trusted Research Environment, TRE) that delivers a simple, interpretable classifier and assesses its equity across demographic subgroups. The work supports Project ID 1077 “Enhancing Diagnostic Equity of Genetic Testing Using Disease Super Panels”.

Objectives
Technical

Data acquisition – obtain de-identified ICD-10 codes, demographics and genetic labels (monogenic vs unexplained) for Brugada cohorts from the Genomics England TRE; ensure access by completing information-governance training as instructed by the supervisor.

Feature engineering – derive patient-level feature sets from ICD-10 codes (counts, temporal patterns, comorbidity indices) and demographics. Exploratory feature families not explicitly mentioned in the documents are annotated as Working Theory.

Modelling – implement baseline models (generalised linear/logistic models and random forest as suggested by the supervisor) and a shallow neural network. Hyperparameters should be tuned via cross-validation.

Evaluation – report discrimination (AUROC, AUPRC), calibration and subgroup performance across sex, age, ethnicity and deprivation, following the equity‐analysis suggestion in JJ’s email.

Reproducibility – track code, random seeds and environment; run analyses within the TRE or ARU HPC and avoid personal laptops.

Academic

Literature review – critically summarise existing approaches to phenotype-based genetic prioritisation and fairness in clinical ML; contextualise Brugada syndrome genetics.

Assessment deliverables – produce a 4 000-word dissertation (85 % of grade), a 1 000-word presentation (10 %) and a 500-word personal development plan (5 %), meeting the thresholds specified in the module definition.

Supervision and record-keeping – attend 12 structured meetings and document progress, as required by the module guide.

Impact

Diagnostic equity – provide evidence that an ICD-10-based proxy does not disproportionately misclassify certain demographic groups. Use fairness metrics (e.g. true-positive-rate parity) and service impact framing per 100 patients (Working Theory).

Service impact view – estimate how many patients could be prioritised for genetic testing, how many referrals might be avoided, and where subgroup differences arise.

Policy awareness – discuss regulatory considerations (e.g. software-as-a-medical-device, data protection) and propose documentation aligned with SaMD frameworks.

Success Metrics

Model performance – Model performance will be evaluated using AUROC and AUPRC (reported with 95 % confidence intervals), balanced accuracy, and calibration curves. Comparative improvement over baseline classifiers will be discussed, but no fixed threshold is imposed; emphasis is on well-calibrated, interpretable, and fair performance across subgroups.

Fairness – difference in true-positive rates and false-negative rates between any two protected subgroups should not exceed 10 percentage points (working threshold). Where disparities arise, document and propose mitigations.

Reproducibility – ability to reproduce results using provided code, dataset splits and random seeds within the TRE.

Academic outcomes – Aim to excel - 85%+ across all assessments; receive positive supervisor feedback.

Constraints & Dependencies

Data access – requires successful completion of GE user-training and information-governance courses and registration as a student on Project ID 1077. (Completed)

Computing environment – analyses must run within Genomics England TRE or the ARU HPC; personal laptops should not be used for heavy compute.

Timeframe – 12-week project window per trimester; data collection may be quick but analysis and write-up are iterative.

Ethics & approvals – rely on existing hospital ethics if patient surveys are included; otherwise the project uses de-identified data (no direct patient contact)【project_description.docx】.

Skill gaps – JJ has limited experience with ML; targeted upskilling in Python, scikit-learn and fairness metrics is required. (In progress)

Risks & Mitigations

| Risk | Mitigation |
| --- | --- |
| Data sparsity & missingness – hospital coding may be incomplete, leading to misclassification. | Perform exploratory data analysis to quantify missingness, use appropriate imputation or exclude low-quality codes. |
| Class imbalance – monogenic cases may be a minority. | Use stratified sampling, reweight classes, and report metrics robust to imbalance (AUPRC). |
| Overfitting & leakage – using future episodes to predict labels could inflate performance. | Define temporal or patient-level splits; ensure no leakage of codes that occur after the genetic diagnosis. |
| Bias & inequity – model may perform differently across demographic groups. | Conduct subgroup analyses, apply reweighting or threshold adjustment, and review features for proxies of protected attributes. |
| Timeline slippage – unforeseen delays in data access or analysis. | Build a sprint log with milestones, maintain regular supervision, and adjust scope if necessary. |
| Skill gaps – complex deep learning may be challenging. | Start with interpretable models; schedule targeted upskilling sessions; consult supervisor or PhD student (Millie Ampiah). |
| Regulatory changes – evolving SaMD or AI-as-a-medical-device rules could impact future deployment【project_description.docx】. | Monitor guidance from MHRA and UK regulators; clearly state that project outputs are for research, not clinical deployment. |

Stakeholders

JJ Zirebwa – final-year biomedical science student and project lead. Responsible for executing the research plan, learning requisite skills and producing deliverables.

Dr Tim Hearn – supervisor at Anglia Ruskin University. Provides subject-matter guidance, data access approvals and project oversight.

Millie Ampiah – PhD student collaborating on related work; potential resource for technical support.

Genomics England TRE team – maintains the secure research environment; approves data access and ensures compliance.

ARU module leader (Christopher O’Kane) & examiners – ensure the project meets academic standards and learning outcomes.

Patients and the wider NHS community – indirect beneficiaries; improved diagnostic pathways could reduce inequities in genetic testing."

