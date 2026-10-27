# Input sources

Gather all four sources in parallel. Every source gets a line in the Input Digest (Step 2 of SKILL.md), even when it returned nothing. A silent gap is the failure this skill most needs to avoid, because a missing source quietly turns into an invented answer.

Tool names differ between surfaces. Use `tool_search` to load the connector tools by capability (for example "google drive search", "fellow meetings", "planhat company", "slack search") rather than assuming a prefix.

## 1. SE handover notes (Google Drive)

- Search Drive with `title contains '<client>'` plus one of: handover, SE notes, sales handover, transition. Drive search uses `title`, not `name`.
- Several matches: prefer the most recently modified, and tell the user which one you used.
- Extract: contract scope (products and plans bought), content types, languages, integrations mentioned, MT/AI intent, legacy assets (TM, TB, style guides), stakeholders, commitments made during the sale, go-live dates.
- Treat sales commitments as requirements to confirm, not facts. Sellers often promise scope that has not been validated.

## 2. SIP data (Slack #sa-sip-early-handover)

SIP data lives in the Slack channel `#sa-sip-early-handover` (channel ID `C0C6VHNLGPL`).

- Search the channel with the client name. Use the Slack search tool with the channel scope (for example `in:#sa-sip-early-handover <client>`), and fall back to reading the channel history and filtering it if search returns nothing. Include likely name variants: legal name, brand or short name, and abbreviations seen in the handover or Planhat.
- For each hit, read the whole thread (`slack_read_thread`), because replies often carry the answers. Note the post date and author.
- Several hits for one client: use the most recent as the baseline and record the older ones as history. Say which you used.
- Join and leave notices in the channel are noise. Ignore them.
- Extract whatever the posts contain that feeds the 11 discovery questions: content types, formats, integrations, teams, assets to migrate, dates, MT/AI intent. Record each fact with the post date.
- Nothing found: set the digest status to "not found in #sa-sip-early-handover" and ask the SA whether SIP data exists elsewhere. Do not guess its contents and do not treat an empty channel as "not applicable".
- The channel is read-only for this skill. Never post, reply or react.

> ⚠️ UNCONFIRMED: which fields SIP posts carry and how they are laid out has not been confirmed, because the channel's recent history held only join notices when this was written. After the first real run, replace this note with the observed format and map its fields to the discovery questions.

## 3. Kick-off meeting notes (Fellow)

- Search Fellow meetings for the client name and "kick-off" / "kickoff". Read the summary first, then the transcript only for details the summary lacks (success criteria, dates, named teams).
- Use the notes only if the kick-off has already happened. Compare the meeting date with the handover document's last-modified date and say which is newer.
- No kick-off yet: continue, but mark the whole plan PROVISIONAL (see SKILL.md Step 6).
- Fellow action items are useful for column F (pre-session tasks from the client) when they are client-owned.

## 4. Planhat

- Look up the Company record. Names can return several matches (for example "NHS"): disambiguate by Company ID and confirm with the user if more than one is plausible.
- Custom fields are not returned by default. Request them explicitly with a SELECT list, for example `custom.Plan Name`, `custom.TMS ID`, `custom.AI Context`, plus ARR, renewal date and CSM owner if available.
- `Plan Name` determines the session budget.

> ⚠️ PLACEHOLDER: the Plan Name → session count mapping has not been defined. Until it is, ask the user how many onboarding sessions the client is entitled to, and record the answer as "user-provided". Never infer a number from the plan tier.

- Read-only in this skill version. Do not write tasks or notes to Planhat (publishing to Planhat is deferred to a later version).

## 5. Hive (Slack #the-hive)

Hive knowledge cards are posted to the `#the-hive` Slack channel as a message plus a threaded reply holding the full card (YAML frontmatter and sections).

- Search `#the-hive` for cards matching the client's situation. Useful frontmatter values: `domain` (client-onboarding, migration, configuration-sequencing, workflow-design, asset-strategy), `vertical`, `content_types`, `mt_engine`, `assets_available`, `client_maturity`, `phase`.
- Read the threaded reply for the card body. Open at most 3 cards; more adds noise.
- Cards with `status: recommended` and `jury-generated` are projected outcomes, not measured ones. If you use one, say so.
- Cards with `needs_review: true` or low `judge_scores` are weak evidence. Prefer others, or flag the weakness.
- Cite by filename in column G (Comments) and in the review summary. No relevant card: say "no matching Hive card" and rely on product documentation.

## Handling conflicts between sources

Newer, client-confirmed information wins over older or seller-written information. When two sources disagree on something that changes the plan (a content type, a go-live date, an integration), list the conflict in the review summary and ask the user to resolve it. Do not choose silently.
