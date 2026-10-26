---
name: sa-onboarding-plan-builder
description: >
  Builds a tailored onboarding plan for a new Phrase customer, for the Solution Architect running
  client enablement. Pulls SE handover notes (Google Drive), SIP data, kick-off meeting notes
  (Fellow) and Planhat data, asks the SA a structured set of discovery questions (pre-filled from
  those sources), then produces a session plan as a Google Sheet based on the Phrase onboarding
  tracker template, paced to the client's urgency and priority content and grounded in Hive cards,
  plus a self-serve guide with Atlas instructions and Help Center / Academy links the client can
  follow on their own. Use whenever an SA says "build the onboarding plan for [client]", "set up
  onboarding for [client]", "onboarding request", "plan the onboarding sessions", "prep the
  onboarding tracker", "create the Atlas self-serve guide for [client]", or names a new client and
  asks how to onboard them, even if the request is vague ("can you sort out onboarding for X?").
  Supersedes onboarding-plan-builder. Does not write to Planhat.
---

# SA Onboarding Plan Builder

Turns what Phrase already knows about a new client into a reviewed, ready-to-run onboarding plan and a self-serve configuration guide. The SA stays in control: the skill gathers, asks, drafts, and stops at a reviewed draft.

**In scope (v1):** gathering inputs, discovery questions, tailored session plan (Google Sheet), self-serve Atlas content (Google Doc).
**Out of scope (v1):** triggering from a request in the SA channel, publishing the approved plan to Planhat, and auditing a client's setup after onboarding (Part 2). If asked, say these are planned for a later version and offer to hand over the approved plan as-is.

## Principles (the reasons behind the steps)

- **Never let a gap pass silently.** A missing source or unknown answer becomes an invented detail unless it is named. Every source and every question gets an explicit status.
- **The template is the maximum, tailoring is subtraction with reasons.** The SA must be able to see what was removed, merged or moved and why, and overrule it.
- **No invented facts or links.** Every client fact traces to a source; every URL was seen in the template baseline or in a search/fetch result during this run.
- **The SA decides.** Nothing is written outside the draft Sheet and Doc, and nothing is sent to anyone.

## Step 0: Identify the client and check tools

1. Get the client name. If not given, ask.
2. Check which tools are available: Google Drive, Google Sheets, Fellow, Planhat, Slack. Use `tool_search` to load them. If one is missing, tell the user which source is affected and continue with a manual fallback (ask them to paste the content). Never skip a source without saying so.
3. Read `references/input-sources.md` now.

## Step 1: Gather inputs in parallel

Fetch these four at the same time, following `references/input-sources.md`:

- SE handover notes (Drive)
- SIP data (PLACEHOLDER source: ask the user to paste or point to it)
- Kick-off notes (Fellow), only if the kick-off has happened
- Planhat company record (Plan Name, TMS ID and other custom fields via explicit SELECT)

## Step 2: Build the Input Digest and show it

Before asking anything, show a compact digest:

| Source | Status | Key facts used | Date / freshness |
|---|---|---|---|

Status is one of: used, partial, not found, not provided, not applicable (kick-off not held). Add a line listing conflicts between sources. If the kick-off has not happened or any source is missing, say the plan will be PROVISIONAL.

## Step 3: Discovery questions

Read `references/discovery-questions.md`. For each of the 11 questions, pre-fill the answer from the digest with source and confidence. Ask only about what is unknown, inferred, or conflicting, in one batch. Use `ask_user_input_v0` for closed questions (max 3 per call) and short prose for open ones.

Also ask, if not already known: the first session date, and the session budget (the Plan Name → session count mapping is a PLACEHOLDER, so ask the SA directly and record "user-provided").

If Q1, Q3 and Q6 are all still unknown after the batch, ask once more before building. If the SA says to continue, continue and mark the plan PROVISIONAL.

## Step 4: Ground in Hive

Search `#the-hive` for cards that fit the client (domain, vertical, content types, MT engine, assets, maturity). Open at most 3. Note filename, what each card suggests (sequencing, gotchas, parameters), and any weakness (jury-generated, `needs_review`, low scores). Use findings to adjust session order, agenda detail and risks. No match: say so and rely on product documentation. Details in `references/input-sources.md`.

## Step 5: Build the plan

Read `references/template-baseline.md` and `references/plan-rules.md`. Then:

1. Select phases and sessions from the answers (rule table in plan-rules.md section 1).
2. Check the count against the session budget. Over budget: propose merges or async work and show trade-offs. Never drop sessions silently.
3. Choose the pacing tier and order sessions. Priority content goes first.
4. Assign dates (weekdays only, async windows for migrations).
5. Fill every column per plan-rules.md section 5. Agendas are tailored to this client. Pre-session tasks are concrete. Comments cite sources and Hive cards.
6. References: reuse links from the baseline. A new link is allowed only if you saw the URL in a search or fetch result in this run (use `phrase-help-fetch` or web search). Otherwise write `TBC - no verified link`.
7. Fix the template defects (missing Phase 7 numbering, "Inegration" typo) and renumber phases contiguously.

## Step 6: Review before creating anything

Present a review summary in chat:

1. **Plan at a glance:** number of sessions, phases, pacing tier and why, first and last dates, budget used / available.
2. **What changed from the template:** removed, merged or moved sessions, each with its reason and the answer or source behind it.
3. **Facts by source:** key client facts with their source and confidence.
4. **Open items:** unknown answers, "scope TBC" sessions, conflicts between sources, and what would change the plan.
5. **Hive cards used** (or "none matched").
6. Whether the plan is PROVISIONAL.

Ask the SA to approve or change it. Apply changes and show the changed rows. Do not create files until the SA says to proceed.

## Step 7: Create the Google Sheet

Read `/mnt/skills/examples/google-workspace/SKILL.md` and `references/sheets.md` in that skill before the first Drive or Sheets call.

- Name: `<Client> - Onboarding Plan (<YYYY-MM-DD>)`. Ask which Drive folder to use if the user has not said.
- Match the template: the same 11 columns in the same order, one tab for the plan. Add a second tab `Summary` holding the review summary (inputs digest, changes from template, open items, Hive cards).
- Dates as real dates. Wrapped text in Agenda, Pre-session tasks, Comments and the reference columns. Frozen header row. A Status dropdown (Not Started, In Progress, Done, Blocked). Arial throughout.
- If PROVISIONAL, put a banner row above the header naming what is unconfirmed.
- Writes parse like the Sheets UI, so check that URLs, IDs and dates came through as intended. Read the Sheet back and verify against the approved plan.

## Step 8: Create the self-serve guide

Read `references/atlas-self-serve.md`, then check the current Atlas Help Center article. Create a Google Doc named `<Client> - Self-serve configuration guide (Atlas)` with one section per in-scope session in plan order. Read the Docs part of the google-workspace skill before the first Docs call. Read the Doc back to verify it.

## Step 9: Close

Link both files in the sentence that says what you did. Give a three-line summary: sessions planned, what is still open, and what needs the SA's review (especially every `TBC - no verified link` and every untested Atlas prompt). State plainly that nothing was written to Planhat or sent to the client. Offer to log the skill run to `#sa-skills-library` via `sa-library-updater` only if the user asks about logging the skill itself.

## Failure handling

- **Source missing or empty:** name it in the digest, ask for a paste, continue as PROVISIONAL if the user has nothing.
- **Planhat returns several companies:** disambiguate by Company ID, confirm with the user.
- **Over budget:** show trade-offs, let the SA choose.
- **Sheets or Drive write fails:** report it, keep the approved plan in chat, and do not create duplicate files on retry.
- **A request to publish to Planhat:** decline for this version, explain it is out of scope, and offer the plan as a Sheet.

## PLACEHOLDERS to resolve (flagged in the files above)

1. SIP data location and fields (`references/input-sources.md`)
2. Planhat Plan Name → session count mapping (`references/input-sources.md`, `references/plan-rules.md`)
3. Preferred self-serve content format (`references/atlas-self-serve.md`)
4. Pacing thresholds (`references/plan-rules.md`) are defaults and need calibration against real engagements
5. Default Drive folder for output files
