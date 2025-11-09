Data Audit Checklist – ICD-10 Brugada Classification

This checklist outlines the data governance, provenance and quality considerations for Project ORION v2. It should be revisited regularly as data are accessed and analysed.

Access & Approvals

Confirm registration with Genomics England under Project ID 1077 and completion of user training.

Ensure supervisor (Tim Hearn) is listed as supervisor in the application; use correct institutional email domains to avoid delays.

Verify that the project falls under existing ethics approvals for secondary analysis; document any additional approvals (e.g. for patient surveys)【project_description.docx】.

Adhere to information-governance and disclosure-control policies when exporting aggregated results from the TRE.

Provenance

Identify dataset owner (Genomics England / NHS) and obtain latest release version of Hospital Episode Statistics and genomic variant calls.

Document refresh cadence: note whether ICD-10 codes are updated yearly and whether variant annotations change.

Record ingestion dates and data versions in the experiment tracker and within metadata files.

Schema Overview

Patient identifier – unique de-identified ID.

Demographics – sex, date of birth or age, ethnicity category, deprivation index/quintile.

Hospital episodes – encounter date, ICD-10 codes, procedure codes, admission/discharge dates.

Genetics – variant call results indicating monogenic (pathogenic variant in SCN5A) vs unexplained.

Diagnosis date – date of genetic diagnosis; used to censor codes to avoid leakage.

Quality Checks

Missingness – assess missing demographic data and absence of episodes; consider imputation or exclusion.

Code sparsity – evaluate distribution of ICD-10 codes; group rare codes into broader chapters to mitigate sparsity.

Date consistency – ensure episode dates precede diagnosis date; remove future codes.

Outlier detection – identify abnormal counts or extreme values (e.g. hundreds of episodes) that may reflect data entry errors.

Leakage risks – exclude codes generated after the genetic label assignment and features directly indicating Brugada (e.g. I49.8) from training if they serve as proxies.

Pre-model integrity tests
• Entity counts preserved pre/post pipeline (overall and by subgroup)
• Forbidden features absent (post-diagnosis, future leakage)
• Windowing/censoring enforced as specified
• Missingness deltas within thresholds
• Label derivation verified from gold sources
• Train/val/test split purity (checksums)
• Reproducibility: seed-fixed re-run within epsilon


Derivations

Feature engineering – document transformations from raw ICD-10 codes to feature vectors, including mapping to chapters, count windows, comorbidity indices and embedding methods.

Label construction – record criteria for monogenic vs unexplained classification, referencing genomic variant annotations and quality filters.

Dataset splits – define training/validation/test partitions at patient level; consider temporal splits to test generalisation; log random seeds and selection criteria.

Reproducibility

Use version control (e.g. Git) for code and documentation; store repositories within the TRE where possible.

Record Python and package versions; capture environment configuration (e.g. via requirements.txt or conda environment files).

Maintain a run ledger in the experiment tracker with dates, model versions, data versions and metrics.

Ensure that any exported results undergo disclosure checks and do not contain identifiable information.

