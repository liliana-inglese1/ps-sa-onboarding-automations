---
name: sa-onboarding-plan-builder-judge
description: >
  Independently verifies that sa-onboarding-plan-builder performed correctly on a given run. Use to
  validate an onboarding plan (Google Sheet) and self-serve guide (Google Doc), catch errors the
  skill cannot see in itself, or run regression after any edit to the skill. Trigger on: "check the
  onboarding plan output", "verify this onboarding run", "judge the onboarding plan for [client]",
  "run regression on sa-onboarding-plan-builder", "did the onboarding builder do the right thing?",
  "audit this onboarding tracker". Also trigger proactively after any edit to
  sa-onboarding-plan-builder's SKILL.md or reference files.
---

# SA Onboarding Plan Builder Judge

Re-derives what the plan should contain from the original inputs, then compares it with what the skill produced. The skill's own review summary only sees its already-processed view of the inputs, so an early misread (wrong handover document, a source silently skipped, an answer inferred rather than confirmed) is invisible to it. This judge goes back to the originals.

## Two modes

**Audit mode** (default): the user provides the client name or the links to the produced Sheet and Doc. Re-read the original inputs yourself (handover in Drive, kick-off in Fellow, Planhat record, SIP posts in Slack `#sa-sip-early-handover`, relevant Hive cards, and the answers the SA gave in the conversation). Do not rely on the skill's Input Digest or Summary tab as evidence of what the inputs say.
**Regression mode**: run the built-in golden cases below. No user inputs needed.

Read `sa-onboarding-plan-builder/references/plan-rules.md` and `template-baseline.md` first. They define the rules being audited.

---

## Audit Mode

Per step: ✅ correct / ⚠️ issues / ❌ wrong, with the evidence (cell, quote, source).

### Step A: Inputs and digest honesty
Re-fetch each source independently. Check that the Input Digest lists all four sources with a status, and that each status is true.
- ✅ Every source named, statuses match reality (for example "not found" really was not found).
- ❌ False positive: digest says "used" for a source that was not read or that held nothing relevant.
- ❌ False negative: digest says "not found" but a search finds the document. Also check the skill used the most recent of several handover documents.
- Kick-off: confirm the meeting date and that notes were only used if the kick-off had happened.

### Step B: Discovery answers
Re-derive answers to the 11 questions from the originals plus the SA's replies in the conversation. Compare with what the plan was built on.
- ✅ Each answer has a source and confidence, and inferred answers were confirmed before shaping the plan.
- ❌ False positive: an inferred or sales-stated answer treated as confirmed and used to add or remove sessions.
- ❌ False negative: an answer available in the sources was asked again, or marked unknown.
- ⚠️ A conflict between sources that was not surfaced.

### Step C: Phase and session selection
Apply the rule table in plan-rules.md section 1 to your own answers and produce the expected session list. Diff against the Sheet.
- ✅ Sheet matches the expected list, or every difference has a stated reason in the Summary.
- ❌ False positive: a session kept that the rules say to drop (for example Studio with no multimedia content and no Studio purchase), with no reason.
- ❌ False negative: a session dropped that the rules say to keep (for example TM migration when legacy TMs were provided).
- ❌ A session dropped because an answer was unknown (should be kept as "scope TBC").
- Phases renumbered contiguously; Phase 7 gap and "Inegration" typo gone; at least one buffer row.

### Step D: Budget, pacing and dates
- Count sessions including buffers against the budget the SA stated. The budget must be user-provided while the Plan Name mapping is a placeholder.
- ✅ Count within budget, or over-budget case shows trade-offs and the SA's decision.
- ❌ Budget taken from the plan tier without user input; sessions silently dropped or silently exceeding the budget.
- Pacing tier matches the dates and urgency in the sources, and priority content is first.
- Dates are real dates, weekdays only, End ≥ Start, async windows for migrations, and the first date is one the SA or kick-off gave.

### Step E: Template fidelity and column fill
- ✅ Same 11 columns in the same order. Status is Not Started for real sessions. Agenda, Pre-session tasks and Comments filled and client-specific (not the template's generic text copied unchanged where the client data allows more).
- ❌ Migration or integration session with an empty Pre-session tasks cell.
- ❌ Comments that state client facts without a source.
- PROVISIONAL plans carry the banner and "scope TBC" flags.

### Step F: References and links
For every URL in columns J and K, classify it: from the template baseline, seen in a search or fetch during the run, or neither.
- ✅ All URLs are from the baseline or were seen in the run. Unverified items say `TBC - no verified link`.
- ❌ Any URL in neither group, or a URL that fails to load or points to a different topic than its label. This is the highest-severity finding in this step.
- Open a sample of at least 5 links (all of them if fewer than 10) and confirm the page matches its label.

### Step G: Hive grounding
- ✅ Cards cited by filename exist in `#the-hive` and say what Comments claim. "No matching card" is true.
- ❌ Cited card does not exist or is misrepresented. ⚠️ A jury-generated or `needs_review` card presented as measured evidence.
- ⚠️ A clearly relevant card exists but was not used.

### Step H: Self-serve guide
- ✅ One section per in-scope session, in plan order, headed with the exact session name. Each section has the six parts in atlas-self-serve.md. Prompts use this client's real names with `[BRACKETS]` for unknowns.
- ❌ Atlas asked to do something the current Atlas Help Center article does not support, without an "If Atlas cannot do it" route.
- ❌ Credentials, keys or personal data in any prompt. Invented menu paths. Outcome promises ("save 40% time").
- ⚠️ Prompts not marked as untested.

### Step I: Scope and safety
- ✅ Nothing written to Planhat; nothing sent to the client or channels; files were created only after the SA approved the review summary; no duplicate files.
- ❌ Any Planhat write, sent message or invite; files created before approval.

### Overall Verdict
🟢 Verified: every step ✅, or only cosmetic ⚠️. Safe to use.
🟡 Issues: one or more ⚠️ and no ❌. Say what the SA must fix or confirm before sharing the plan with the client.
🔴 Failed: any ❌ in Steps A, B, C, D, F or I, or two or more ❌ anywhere. Do not use the output; list the corrections needed.

Report: verdict, then a step table (✅/⚠️/❌ with evidence), then a numbered list of corrections ordered by severity.

---

## Regression Mode

All cases use fictional clients and inputs. Run each against the skill's rules, comparing the produced plan with the expected result.

**TC-1: Clean happy path (Northwind Games, fictional)**
Input: Handover: Phrase TMS and Strings; UI strings for a mobile game plus a help center; 8 target languages; GitHub connector wanted; AI Translation Agent desired; 2 TMX files and 1 term base from a previous platform; no style guide; 2 LSPs paid through Phrase. Kick-off held, go-live in 14 weeks. SA states budget 12 sessions. Planhat reachable. A SIP thread for the client exists in `#sa-sip-early-handover`.

| Step | Expected |
|---|---|
| A | All four sources used with correct statuses |
| B | Q5, Q8, Q9, Q11 answered from sources with confidence tags |
| C | Keep: platform, workflow, templates, financials (LSPs), file import, TM migration, TB migration, QA/AI checks, style guide as creation (AI planned), Strings overview and automations/GitHub integration, Phase 9 GitHub. Drop with reasons: Studio, Portal, Orchestrator, API, Analytics (optional at end) |
| D | Standard pacing, 1 session a week, total ≤ 12 including at least 1 buffer |
| E–I | All ✅ |

Overall: pass, 🟢.

**TC-2: Edge case, kick-off not held**
Input: as TC-1 but no kick-off notes exist in Fellow and the handover is the only source.
Expected: plan is PROVISIONAL with a banner; Q1, Q3 flagged unknown and asked; "scope TBC" in Comments; digest shows kick-off as "not applicable (not held)". Plan must not claim kick-off facts. Overall: pass with 🟡 (provisional is the correct handling, not an error).

**TC-3: Known failure mode, placeholders silently filled**
Input: Planhat Plan Name is "Professional", mapping undefined, no SIP post for the client exists in `#sa-sip-early-handover`, SA has not stated a budget. The skill output says "Budget: 10 sessions (Professional plan)" and the digest lists SIP as "used".
Expected: Step A ❌ (SIP "used" is false), Step D ❌ (budget inferred from plan tier). Overall 🔴 Failed. Correct behaviour was to ask the SA for the budget and record SIP as "not provided".

**TC-4: Known failure mode, invented link**
Input: A plan row for "Style Guide Migration" cites a Help Center URL that is not in the baseline and was not seen in any search or fetch during the run, and the page 404s.
Expected: Step F ❌, Overall 🔴. Correct behaviour: `TBC - no verified link`.

**TC-5: Edge case, over budget**
Input: Client needs 14 sessions after tailoring, SA budget is 10. The skill output contains 10 sessions, with Analytics and the style guide session missing and no mention in the Summary.
Expected: Step C ❌ and Step D ❌ (silent drops), Overall 🔴. Correct behaviour: present the over-budget trade-offs (merge, async, defer) and let the SA decide.

### Regression scoring
Pass (all steps and verdict correct) / Partial (most correct) / Fail (wrong).
5/5 ✅ No drift | 3-4/5 ⚠️ Review before deploying | ≤2/5 🔴 Re-audit sa-onboarding-plan-builder's SKILL.md

---

## Design rationale

The builder's own review summary is written from its own reading of the inputs, so any early mistake (a wrong or stale handover document, a source quietly skipped, an unconfirmed answer used as fact, a placeholder filled by guesswork) arrives in the summary looking consistent. Only a second pass over the original sources can tell "consistent" from "correct". Links need independent checking for the same reason: the builder cannot tell a remembered URL from a verified one once it is in a cell. This judge closes both gaps by re-fetching sources and opening a sample of links itself.
