# Plan rules

The template (`template-baseline.md`) is the maximum plan. Tailoring means removing, merging, reordering and re-pacing sessions with a stated reason, not rewriting the structure. Every removed or merged session is listed in the review summary with its reason, so the SA can overrule it.

## 1. Phase and session selection

| Template item | Keep when | Otherwise |
|---|---|---|
| Phase 1 Platform onboarding (users, SSO, Atlas) | Always. Shorten to a refresher if Q4 shows experience | Never remove |
| Workflow steps + project metadata | Phrase TMS is in scope | Drop with TMS |
| Project templates | Phrase TMS is in scope | Drop with TMS |
| Financials: net rate scheme, price lists | Client pays vendors or linguists through Phrase (Q9) | Drop; note "revisit if vendor model changes" |
| File import settings, segmentation, placeholders, ICU | File-based or string content in TMS (Q6, Q7) | Drop only if integrations deliver all content and no file import is used |
| TM migration | Legacy TMs will be provided (Q11) | Replace with a short "TM creation and sharing" agenda inside the Project templates session |
| QA / AI Checks / LQA | MT or AI in use or desired (Q5), or quality is a success criterion (Q1) | Merge into Workflow session as a short agenda item |
| Style guide migration | Style guides provided (Q11) or AI translation planned (Q5) | Drop |
| Term base migration | Legacy TBs provided (Q11) | Replace with "TB creation" agenda item |
| Phase 2 Analytics | Reporting, cost or volume tracking appears in success criteria (Q1) | Put at the end of the plan as optional |
| Phase 3 Studio | Studio is purchased or multimedia content is in scope (Q6) | Drop |
| Phase 4 Portal | Phrase Portal is purchased, or requesters submit content outside TMS (Q6, Q9) | Drop |
| Phase 5 Orchestrator | Automation is needed (Q5, Q10) or an integration workflow needs it | Drop |
| Phase 6 Strings | Software UI strings are in scope (Q6) or Strings is purchased | Drop |
| Phase 8 API | Custom tooling or API use (Q10) | Drop |
| Phase 9 Integration | An out-of-the-box connector is planned (Q8). Name the connector in the phase and session titles | Drop |
| Phase X buffers | Keep 1 to 3 depending on budget; always at least 1 | Never remove all |

If purchase scope (which Phrase products the client bought) is unknown, keep the phase and mark "scope TBC" in Comments. Do not infer purchase scope from plan tier.

Renumber phases contiguously after removals (Phase 1, 2, 3, ...). The template skips Phase 7 and has the typo "Inegration"; fix both. Keep the label pattern `Phase N -- Team Enablement & <Product> Configuration`, and keep `Phase X -- Reserved / Buffer Sessions` for buffers.

## 2. Session budget

- Count sessions after tailoring. Buffers count toward the budget.
- If the count exceeds the budget, propose merges or async work and list the trade-offs. Never drop sessions silently to fit, and never exceed the budget silently.
- The budget comes from Planhat Plan Name through the mapping, which is a PLACEHOLDER (see `input-sources.md`). Until the mapping exists, the budget is whatever the user states.

## 3. Pacing

Pick a pacing tier from Q3 (milestones and dates) and Q1 (urgency). These thresholds are defaults for the SA to override. State the tier and the reason in the review summary.

| Tier | Trigger (default) | Cadence | Ordering |
|---|---|---|---|
| Urgent | Hard go-live date within about 8 weeks, or client flags priority content | Up to 2 sessions a week | Critical path first: platform, workflow, templates, file import, then the first integration. Migrations and analytics run async in parallel or after go-live |
| Standard | Go-live 8 to 16 weeks away, or a soft target | 1 session a week | Template order, with priority content pulled forward |
| Relaxed | No date | Every 1 to 2 weeks | Template order, clustered by phase |

Priority content (Q6) moves its workflow, template and integration sessions to the front of the plan, whatever the template order says.

## 4. Scheduling

- Ask for the first session date if neither the kick-off notes nor the user gave one.
- Weekdays only. A synchronous session has the same Start and End date. An async session (TM, TB or style guide migration) gets a window, with End Date at least 2 working days after Start.
- Dates are real date values in the Sheet, not text.
- Do not schedule across dates the client named as unavailable (freezes, holidays). If you do not know their calendar, say the dates are proposed and unconfirmed.
- Never write calendar invites. Scheduling here means filling Start and End dates.

## 5. Filling the columns

| Column | Rule |
|---|---|
| A Phase | Label on the first row of each phase only, as the template does for phases with several sessions. Buffers repeat their label on each row |
| B Session | Template wording, adapted with client specifics (connector name, product names) |
| C, D Dates | Per section 4 |
| E Agenda | `Main: ...` and, where useful, `Other: ...`. Tailor to this client's content types, formats, teams and assets. Do not leave the template's blank agendas blank |
| F Pre-session tasks from client | Concrete, checkable client deliverables: files to provide, access to grant, decisions to make, people to invite. Pull client-owned Fellow action items. Never leave blank for a migration or integration session |
| G Comments | Source of key facts (handover / kick-off / Planhat / user), PROVISIONAL or "scope TBC" flags, Hive card filenames used, risks |
| H Status | `Not Started` for every real session. Buffers stay blank as in the template |
| I Meeting recordings | Leave blank |
| J HC article | `Title - URL` pairs separated by ` | `. Reuse links from `template-baseline.md`. A new link is allowed only if you saw the URL in a search or fetch result in this run (use the `phrase-help-fetch` skill or a web search). Otherwise write `TBC - no verified link` |
| K Academy module | Same rule as J. Academy links come from the baseline or a search of training.phrase.academy |

Never invent a URL. A plausible-looking dead link is worse than a visible TBC, because the client will click it.

## 6. Provisional plans

A plan is PROVISIONAL when the kick-off has not happened, a source was missing, or any of Q1, Q3, Q6 is unknown. A provisional plan carries a banner row at the top of the Sheet, uses "scope TBC" in Comments where relevant, and names in the review summary exactly what would change the plan.
