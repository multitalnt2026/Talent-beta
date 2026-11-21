# Talent – working rules

Talent is a Hebrew (RTL) marketplace app prototype in a single file, `index.html`. Two user types: talents (כישרונות) offer services; scouts (סקאוטים) browse, like, save and book.

## How the owner works

- **The build happens in the Claude chat** (the owner's saved project chat). That is the only conversation.
- **The workspace is a status board, not a second chat:** https://claude.ai/artifact/9Gs5fhgSFLphixd31ZoY1H
  - "App" tab: what is approved now, the changes in progress since the last approved version, and an approve button.
  - The orange "enter app" button opens the approved version with the highest `n`.
  - "Ideas" tab: the owner's idea notebook.
- Presentation doc (Claude Docs): https://claude.ai/artifact/Y1dY32SyxKXpLLzhjkU2XB

## Workspace database (what the page reads)

- `state/draft`: changes in progress, not approved yet. `{title, changes: [..], summary, url, github, overview: [{h, items: [..]}], updatedTs}`.
  `changes` = short Hebrew lines describing what differs from the last approved version. `overview` = the whole product as it will be once approved.
- `state/product`: overview of the approved product `{n, overview, updatedTs}`. The page copies it from the draft on approval.
- `versions/vN`: `{n, title, summary, changes, url, github, status: "approved", ts, approvedTs, processed, docUpdated, ideas}`. History; never edit an approved version's `url`.
- `state/doc`: read-only copy of the presentation doc's APPROVED text for the split-screen panel `{blocks: [{t: "h1"|"h2"|"p", x} | {t: "ul"|"ol", i: [..]} | {t: "table", r: [[..]]}], rev, syncedTs, pending}`. Inline `**bold**` and `[text](url)` only. Leave out pending suggestions; `pending` = how many are open.
- Workspace files: each version's app is also published INTO the workspace artifact as `vN.html` (same-origin, so the split-screen demo can embed it). `versions/vN.file` and `state/draft.file` point to it.
- `ideas`: the notebook. `state/live`: optional "Claude is working on…" banner (`active`, `title`, `steps`).
- No longer shown by the page: `turns`, `decisions`, `app/*`, `chat`/`sep` entries in `ideas`. Don't write them.

## Each round

1. At the start, read `versions` for an approval with `processed: false`. If found: set `processed: true`, record the version in this file, and start the next draft on a NEW artifact.
2. Make the code change in `index.html`, test it, commit and push to `claude/map-tab-modern-ui-omcquc`.
3. Publish the draft: copy `index.html` to `versions/vN/index.html` in the scratchpad (N = next version) and publish with `capabilities: {downloads: true}`. While a draft is unapproved, republish to the same draft path (same URL). Never republish an approved version's URL.
4. Publish the same `index.html` into the workspace artifact as `vN.html` (`files: {"vN.html": <path>}`), then write `state/draft` with the cumulative `changes` since the last approved version, the draft `url`, `file: "vN.html"`, and the full `overview`.
5. Presentation doc: suggestions only (suggestion mode), so nothing replaces approved text until the owner accepts it. At the start of a round, if the doc's approved text changed (suggestions accepted or edits), rewrite `state/doc` from it.
6. If the owner approves in chat instead of the button: write `versions/vN` (approved, `processed: true`), copy `overview` to `state/product`, delete `state/draft`.

## Rules from the owner

1. **Don't guess.** When a request can be read more than one way, send two options in the chat and let the owner pick. If neither fits, they correct that topic.
2. Nothing replaces the approved app version or approved doc text until the owner approves it.
3. Keep the base look: teal brand, coral CTA, Rubik font, light and dark themes.

## Versions so far

- v1 https://claude.ai/artifact/4izUUqA3zdZSienS9thcn4 · v3 https://claude.ai/artifact/KyPhBFZcPWFohzmJa9fDmL · v4 https://claude.ai/artifact/8Cn8tfUuX4xza3pnPX8m3B
- v5 (approved, current) https://claude.ai/artifact/Vu4c21krzPXQiRQDMwsQff · next draft = v6
