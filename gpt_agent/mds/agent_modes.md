Agent Modes – Project ORION v2

Project ORION v2 operates in several modes to manage tasks systematically. Modes can be invoked by the user or automatically by the project instruction block when certain conditions are met.

Mode Definitions
1. Research

Default until an Agent execution plan exists: Research. Switch to Build only after the plan is adopted. Supervision only in week of a scheduled meeting or when a decision awaits sign-off.

Purpose – Survey literature, methods and policies relevant to the project.

Entry criteria – Invoked explicitly by the user (e.g. “Mode: Research”) or triggered when reading_triage.md contains unreviewed items and there is no ongoing experiment.

Inputs consumed – Topics and sources from reading_triage.md (status “to read” or “reading”); user-provided queries.

Outputs produced – Summaries of papers, notes appended to reading_triage.md (status updated to “digested”), and citations in subsequent artefacts.

Done definition – Completed when targeted items have been read and summarised; status updated; user receives a summary or report.

2. Build

Purpose – Construct the data pipeline, engineer features and train models.

Entry criteria – Invoked by user (e.g. “Mode: Build”) or automatically when data access is confirmed and there is an experiment in progress or pending.

Inputs consumed – Cleaned data from TRE, feature definitions from ontology_map.md, model choices and decisions.

Outputs produced – Updated code notebooks/scripts, trained models, metrics recorded in experiment_tracker.md and new entries in decisions.md as needed.

Done definition – Exit when a model has been trained, evaluated and logged; readiness for supervision or equity analysis triggers transition to other modes.

3. Equity

Purpose – Perform subgroup performance analysis and implement fairness mitigations.

Entry criteria – Called by user or automatically after each major model experiment (e.g. when new metrics are logged and fairness analysis has not been performed).

Inputs consumed – Experiment results (metrics), subgroup definitions from equity_plan.md and decisions regarding fairness thresholds.

Outputs produced – Subgroup metrics, mitigation actions (e.g. threshold adjustments) recorded in experiment_tracker.md and updates to equity_plan.md.

Done definition – When disparities have been quantified and, if necessary, mitigated; results documented and communicated.

4. RegPolicy

Purpose – Address ethics, data governance and regulatory documentation.

Entry criteria – Triggered when policy questions arise, new data sources are added, or regulatory guidance changes; can be invoked by user.

Inputs consumed – governance_card.md, data_audit_checklist.md, relevant policy documents.

Outputs produced – Updated governance card, data audit checklist and reports on regulatory updates; guidance for supervisor.

Done definition – Completed when necessary documentation is updated and compliance questions are resolved.

5. Supervision

Purpose – Prepare materials for supervisory meetings and implement feedback.

Entry criteria – Default mode when no other mode is requested and a meeting is scheduled within five calendar days; invoked by user.

Inputs consumed – Latest experiment tracker, decisions log, reading triage and sprint log.

Outputs produced – A filled supervision pack (see supervision_pack_template.md), updated sprint log and action items.

Done definition – Exit when the supervision pack is delivered and meeting outcomes are incorporated into project artefacts.

6. Upskill

Purpose – Provide targeted learning plans to address skill gaps identified during the project.

Entry criteria – Triggered when the user requests help with a specific tool or method, or when the build or research mode encounters a blocker due to missing knowledge.

Inputs consumed – Description of the blocker, current skill level and relevant sections of reading_triage.md.

Outputs produced – A micro-curriculum (≤3 resources) with practice tasks tied to the project; updates to reading_triage.md and sprint_log.md.

Done definition – Completed when the user completes the prescribed learning and reports back; progress is reflected in subsequent build or research tasks.

Mode Transitions

Modes may transition according to the following logic:

If an experiment is in progress, stay in Build until the model is trained; then transition to Equity for fairness analysis; then to Supervision for review.

If new literature is identified or items remain in reading_triage.md, prioritise Research before starting a new experiment.

If fairness analysis identifies significant disparities, loop between Equity and Build to implement mitigations and re-evaluate.

If ethics or regulatory issues emerge, temporarily switch to RegPolicy.

After supervisory meetings, return to the appropriate mode (Research or Build) based on agreed next steps.

