Supervision Pack Template

Use this one-pager for each supervisory meeting. Complete the sections below and circulate to the supervisor at least 24 hours before the meeting. Focus on method-development + evaluation, document iteration history, and report TRE data-integrity status. Do not include timeline commitments unless an approved execution plan exists.

| Field | Description |
|---|---|
| Version / Meeting date | Specify template version (e.g. v1.0) and date of meeting. |
| What changed since last meeting? | Summarise work completed: data access milestones, experiments run, literature digested, code updates. Reference experiment IDs, decisions or reading triage items as needed. |
| Results | Present key findings (e.g. model metrics, subgroup analyses). Include concise tables or graphs if possible; adhere to disclosure controls. |
| Streams status (Method & Analysis) | Brief status for each stream: Method-development (what iteration you’re on; key change since last meeting) and Data-analysis (dataset readiness; any summaries). Link to relevant notebook/commit IDs. |
| Data integrity & TRE compliance | Tick-box summary of integrity checks (entity counts preserved; no post-diagnosis features; windowing enforced; missingness deltas; label hygiene; split purity; reproducibility). Note pass/fail, link to test report, and confirm only disclosure-controlled aggregates left the TRE. |
| Process log & decisions updates | New experiment IDs added to the experiment tracker since the last meeting (IDs only) and any decisions.md entries created/updated (IDs). Keep detail out of the pack; link to the source files. |
| Export summary (since last meeting) | List any aggregated outputs exported from the TRE (file name/figure type, approval reference if applicable). If none, state “None”. |
| Risks / asks | Highlight risks or blockers (e.g. data delays, performance issues, skill gaps) and request support or decisions from the supervisor. |
| Upcoming milestones | List goals for the next period (e.g., integrity checks, baseline runs, fairness analysis, drafting sections). Align to the current approved execution plan; if none exists yet, note “Pending Agent execution plan” and leave milestones as N/A.|
| Decisions pending | Identify decisions requiring supervisor input (e.g. change of model, ethical considerations, scope adjustments). Reference entries in decisions.md. |

Include a “Version history” section at the end if multiple iterations of the supervision pack are created.