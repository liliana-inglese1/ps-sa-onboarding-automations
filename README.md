# ps-sa-onboarding-automations

Claude skills that automate Solution Architect client-onboarding work at Phrase.

## Skills

| Skill | Status | What it does |
|---|---|---|
| [`sa-onboarding-plan-builder`](skills/sa-onboarding-plan-builder) | Draft v0.1, not yet piloted on a real client | Builds a tailored onboarding plan (Google Sheet) and a self-serve Atlas guide (Google Doc) from SE handover notes, SIP data, kick-off notes and Planhat. Asks 11 discovery questions, grounded in Hive cards |
| [`sa-onboarding-plan-builder-judge`](skills/sa-onboarding-plan-builder-judge) | Draft v0.1, regression cases not yet run | Companion judge: re-reads the original sources and audits a produced plan and self-serve guide; includes 5 golden regression cases |

## Working on a skill

1. Create a branch, edit files under `skills/<skill-name>/`, open a PR.
2. Keep `SKILL.md` under 500 lines; put detail in `references/`.
3. The `description` in the frontmatter must stay under 1,024 characters.
4. Record every change in `CHANGELOG.md`.

## Packaging

A `.skill` file is a zip of the skill folder. Do not commit it. Build it with the skill-creator packaging script:

```bash
python -m scripts.package_skill skills/sa-onboarding-plan-builder ./dist
```

## Data rules

- This repo holds skill definitions only. **No client data, plans, transcripts, Planhat exports or personal data.** Per Phrase policy, never commit PII to a GitHub repo without an explicit warning and override.
- Test runs and generated plans stay in Drive, not here.

## Open placeholders (track as issues)

1. SIP data: location and fields
2. Planhat Plan Name -> session count mapping
3. Preferred self-serve content format
4. Pacing thresholds (urgent / standard / relaxed) need calibration
5. Default Drive output folder
