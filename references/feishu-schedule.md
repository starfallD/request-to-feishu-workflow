# Feishu and scheduling reference

## Feishu document state

Use these states precisely:

- `draft`: content is being prepared locally;
- `created`: the Feishu API returned a document URL;
- `verified`: `docs +fetch` confirmed the intended content;
- `failed`: creation or verification returned an error.

For a new authored document, the `lark-doc` workflow is: presentation decision, `+script init-draft`, write XML, `+script parse`, `+create`, then `+fetch`. Do not skip parse or fetch because the document is short.

## Automation state

Use these states precisely:

- `suggested`: a scheduler suggestion was rendered;
- `awaiting confirmation`: the user still needs to confirm the suggestion card;
- `active`: the automation tool confirmed it is enabled;
- `paused`: the automation exists but will not run;
- `failed`: creation or update was rejected.

A future first run must be represented by an anchored schedule or a scheduler confirmation flow that preserves the requested start date. A plain weekly rule without a start boundary is unsafe when the user says “not this week” or gives a future start date.

The scheduled prompt must state:

- the selected research skill and source priorities;
- the exact output destination;
- whether to create a new Feishu document or update an existing one;
- whether the full report stays out of chat;
- the short success or failure response.
