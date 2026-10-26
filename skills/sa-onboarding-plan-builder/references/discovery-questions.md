# Discovery questions

Ask these after the Input Digest is built. Pre-fill every answer the sources already give, tagged with its source, and ask only about what is missing or conflicting. Asking a client-facing SA to repeat what is in the handover notes wastes their time and teaches them to ignore the skill.

Ask in one batch (use `ask_user_input_v0` for the closed questions, at most three per call, and short prose for the open ones). Do not run eleven sequential turns.

| # | Question | What it drives in the plan |
|---|---|---|
| 1 | Success criteria outlined by the client | Order of phases, definition of done per session, what goes in the review summary's "success measures" |
| 2 | Current teams and departments involved | Who attends which session; Phase 1 user and role design; split of sessions by audience (PMs, linguists, developers, marketing) |
| 3 | Known milestones and target dates for production enablement | Pacing tier (see plan-rules.md), start/end dates, which sessions are compressed or run async |
| 4 | Previous experience with Phrase products (which exactly) | Skip or shorten introductory sessions; Academy links become "refresher" instead of "prerequisite" |
| 5 | Current and desired use of MT and AI | QA / AI Checks / LQA session, AI optimization session in Phase 9, Orchestrator inclusion, Studio relevance |
| 6 | Content types and workflows in scope | Which phases are in scope at all (TMS, Strings, Studio, Portal), workflow design depth, project templates |
| 7 | File formats the client works with | File import settings session depth; flag formats that need a Blueprint (see tms-import-suite skills) |
| 8 | Out-of-the-box integrations Phrase supports | Whether Phase 9 is included and which connector it covers; pre-session tasks for credentials and access |
| 9 | Vendor strategy (freelancers, in-house linguists, LSPs) | Net rate scheme / price lists session, external agency user management, Portal inclusion |
| 10 | Potential integrations or custom tooling | Phrase API and Orchestrator phases; flag anything beyond standard connectors as a scoping risk |
| 11 | Legacy data to migrate (TMs, TBs, style guides) from previous platforms | TM migration, TB migration, style guide migration sessions; async work and file-cleaning tasks as pre-session items |

## How to pre-fill

For each question write: **answer**, **source** (handover / SIP / kick-off / Planhat / user), and **confidence** (confirmed by the client, stated by sales, inferred). Inferred answers must be shown as inferred and confirmed with the user before they change the plan.

## When an answer is "unknown"

Unknown is a valid answer. Record it, keep the related sessions in the plan marked "scope TBC" in Comments, and list the question under Open Items in the review summary. Do not drop a session on an unknown, and do not keep it as if confirmed.

## Interaction rules

- Offer the pre-filled answers back for a quick "correct / change" pass instead of asking each question cold.
- If the user says to proceed with gaps, proceed and mark the plan PROVISIONAL.
- Questions 1, 3 and 6 change the structure of the plan the most. If those three are still unknown after the batch, ask once more before building.
