Ontology Map – ICD-10 Brugada Classification

This ontology outlines the key entities and relationships for Project ORION v2. It serves as a conceptual model to guide data integration and feature engineering.

Entities
| Entity | Description |
|---|---|
| Patient | A de-identified individual enrolled in the Brugada cohort. Each patient has demographic attributes (sex, age, ethnicity, deprivation). |
| Encounter / Hospital Episode | A single admission or outpatient episode recorded in Hospital Episode Statistics. Each encounter contains one or more ICD-10 codes and timestamp information. |
| ICD-10 code | A diagnostic code assigned during an encounter. Codes are standardised and hierarchical (I49.8 code for "Other specified cardiac arrhythmias" - which includes Brugada syndrome.) |
| Feature | Derived variable representing a patient’s medical history, e.g. counts of codes, time since first code, comorbidity indices, or embedding representations. |
| Genetic label | Binary indicator denoting whether the patient has a monogenic Brugada presentation (e.g. pathogenic variant in SCN5A) or is unexplained【project_description.docx】. |
| Subgroup | A category based on protected attribute values (sex, age group, ethnicity, deprivation quintile) used for fairness analysis. |
| Model | A statistical or machine-learning algorithm (e.g. logistic regression, random forest, neural network) that maps features to a probability of monogenic status. |
| Metric | Quantitative measure of model performance (e.g. AUROC, AUPRC, calibration error, fairness disparity). |
| Decision | Choice recorded in the decision log (e.g. label definition, model selection, split strategy). |

Relations

patient → encounter – A patient has zero or more encounters.

encounter → ICD-10 code – Each encounter may include multiple ICD-10 codes. Codes include the diagnosis, procedure and cause of admission.

patient → feature – Features are aggregated at the patient level from their encounters (counts, temporal patterns, comorbidity indices). A patient may have many features.

patient → genetic label – Each patient has exactly one genetic label (monogenic/unexplained).

patient → subgroup – Patients belong to subgroups based on demographic attributes; one patient can belong to multiple subgroup categories.

feature + model → prediction – A model consumes the feature vector and outputs a predicted probability and class.

prediction + genetic label → metric – Metrics are computed by comparing predictions with ground truth and aggregated overall and per subgroup.

decision → model / data / metrics – Decisions capture choices about label definitions, feature sets, modelling approaches and evaluation methods.

Feature Families

The following feature families will be explored; those not explicitly described in the source documents are marked as (Working Theory).

1. Count features – For each ICD-10 code (or grouping), compute the number of times it appears for a patient within a defined window. For rare codes, group into broader chapters.

2. Temporal patterns – Capture recency and trajectory of codes, e.g. time since first occurrence, number of distinct codes per year (Working Theory).

3. Comorbidity indices – Calculate indices such as the Charlson Comorbidity Index or Elixhauser Score from ICD-10 codes (Working Theory).

4. Demographic features – Include age at recruitment, sex, ethnicity and deprivation. Demographics can interact with ICD-10 features.

5. Embedded representations – Transform code sequences into embeddings via methods such as Word2Vec or autoencoders (Working Theory). Use caution due to limited time and compute.

Data Lineage Stubs

1. Source data – Hospital Episode Statistics and genomic variant classifications retrieved from Genomics England TRE under Project ID 1077.

2. Ingestion – Data extracted within the TRE; patient identifiers removed; episodes joined to create a longitudinal record per patient.

3. Pre-processing – Map ICD-10 codes to standard chapters; remove codes occurring after the genetic test date to prevent leakage; handle missing demographic information.

4. Feature engineering – Generate feature families described above; normalise or scale as required; store feature matrices with metadata.

5. Dataset splits – Create training, validation and test splits at the patient level, ensuring no overlap. Consider temporal splits to avoid future information leakage.

6. Modelling & evaluation – Train models using training data; tune hyperparameters on validation set; report performance on hold-out test set; compute subgroup metrics.

7. Outputs & storage – Save model weights, performance reports and experiment metadata within the TRE; export aggregated, disclosure-checked results according to Genomics England policy.

