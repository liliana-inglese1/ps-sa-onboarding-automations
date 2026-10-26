# Self-serve content with Atlas

Phrase Atlas is a conversational AI agent inside the Phrase platform. The user describes an outcome in natural language and Atlas carries it out. Per the Phrase Help Center it asks for confirmation before making changes, respects the user's existing organization, role and project permissions, and everything it creates stays visible and editable in the platform. It is reachable from the main navigation and from the Ask Atlas button in the Platform Dashboard, Phrase TMS and Phrase Strings.

Before writing a guide, check the current Atlas article in the Help Center (use the `phrase-help-fetch` skill on the Phrase Atlas article, or a web search). Atlas is new and its capabilities and plan availability change. A guide that tells a client to ask Atlas for something it cannot do is worse than no guide.

> ⚠️ PLACEHOLDER: the team's preferred format for client-facing self-serve content has not been confirmed. The format below is a sensible default. If the SA supplies an existing house style, follow that instead and update this file.

## Output

One Google Doc per client, named `<Client> - Self-serve configuration guide (Atlas)`. One section per in-scope session, in the same order as the plan, headed with the exact session name from the Sheet so the two can be cross-referenced. Out-of-scope and "scope TBC" sessions get no section (list them at the end under "Coming later").

## Section template

For each session:

1. **Goal.** One sentence, plus what "done" looks like in terms the client can check themselves.
2. **Before you start.** Required role or permission, files or information to have ready (match column F of the plan), and who in the client's team should do this.
3. **Steps.** For each step:
   - **Ask Atlas:** a prompt the client can paste, written with this client's real names, content types and languages, and `[BRACKETS]` wherever a value is unknown.
   - **Review before you confirm:** what Atlas's proposed plan should contain, and what to reject.
   - **Check in Phrase:** where in the platform to verify the result (menu path or object name).
4. **If Atlas cannot do it.** The manual route in one or two lines, with the Help Center link.
5. **Learn more.** HC and Academy links from the plan's J and K columns for this session.
6. **Book a session when.** The conditions under which the client should wait for the session with the SA rather than continue alone (for example anything touching SSO, production data, or vendor rates).

## Rules

- Only describe things Atlas is documented to do. When unsure, route to "If Atlas cannot do it" instead of promising.
- Mark every prompt "not yet tested against this client's account" unless the SA confirms they ran it.
- No credentials, API keys, tokens or personal data in prompts or examples. Use `[PLACEHOLDER]` values.
- Do not give the client advice that bypasses their own approval steps (for example publishing to production, deleting data, changing rates). Say these need a review first.
- Keep language plain. The reader is a client project manager or localization lead, not a Phrase SA.
- Never invent menu paths. Use paths from the Help Center article you read in this run. If you did not read one, describe the location generically ("the project templates area of Phrase TMS").
- Do not claim an outcome (time saved, quality gains). The guide gives instructions, not promises.

## Worked mini-example (shape only)

Session: *Establish setup for projects (Project Templates)*

> **Goal:** One project template per content type, ready for PMs to create projects from. Done = a PM can create a project for [CONTENT TYPE] using the template without choosing settings by hand.
> **Before you start:** Project manager role or higher. Have the workflow steps, target languages and TM/TB names you agreed in the previous session.
> **Ask Atlas:** "Create a project template called [CLIENT] - [CONTENT TYPE] with source language [SOURCE], target languages [TARGETS], the workflow [WORKFLOW NAME], and the translation memory [TM NAME]."
> **Review before you confirm:** Check the languages and workflow listed in Atlas's plan match the ones above. Reject if it proposes creating a new workflow you did not ask for.
> **Check in Phrase:** Open the new template in Phrase TMS and confirm the languages, workflow and TM.
> **Book a session when:** you need vendor assignment rules or net rate schemes built into the template.
