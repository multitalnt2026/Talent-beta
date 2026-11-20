# Talent – working rules

Talent is a Hebrew (RTL) marketplace app prototype in a single file, `index.html`. Two user types: talents (כישרונות) offer services; scouts (סקאוטים) browse, like, save and book.

## Where things live

- Workspace (the owner's home for the project): https://claude.ai/artifact/9Gs5fhgSFLphixd31ZoY1H
  - The page was rebuilt (21.11.2026) and reads these collections:
    - `versions/vN`: `n`, `title`, `summary`, `url`, `status` (`pending` | `approved` | `changes`), `ts`, `approvedTs`, `ideas`, `processed`, `docUpdated`, `github`. The orange button opens the approved version with the highest `n`; the history sheet lists them all.
    - `turns`: the work conversation (`role` me/claude, `text`, `ts`, `status`, `steps`, `source`). Messages typed in the workspace arrive with `status: "queued"`.
    - `decisions`: open choices with two options (`q`, `ctx`, `a`, `b`, `status` open/answered, `choice`, `note`).
    - `ideas` (ideas chat; older work logs as `chat`/`sep` entries), `state/live` (what Claude is doing now).
    - `app/*` is the old format and is no longer read by the page.
- App pages: each version is its own artifact, so the approved one never changes under the owner.
  - Approved (as of 21.11.2026): https://claude.ai/artifact/Vu4c21krzPXQiRQDMwsQff (version 5). Never republish an approved version's URL.
  - Earlier: version 3 https://claude.ai/artifact/KyPhBFZcPWFohzmJa9fDmL, version 4 https://claude.ai/artifact/8Cn8tfUuX4xza3pnPX8m3B (superseded by 5).
  - A new version: copy `index.html` to a new path in the scratchpad (e.g. `versions/v5/index.html`) and publish it as a NEW artifact with `capabilities: {downloads: true}`; that URL goes into a new `versions/vN` doc with `status: "pending"`.
- Presentation doc (Claude Docs): https://claude.ai/artifact/Y1dY32SyxKXpLLzhjkU2XB

## Rules from the owner

1. **Don't guess.** When a request can be read more than one way, send two options and let the owner pick. If neither fits, they correct that topic.
2. **App versions need approval.** After code changes: commit and push, publish the new version as its own artifact, then write `versions/vN` with `status: "pending"`. The owner approves (or asks for changes) with the buttons in the workspace, or in chat. Only set `status: "approved"` yourself when the owner says the version is approved. After acting on an approval or change request, set `processed: true`.
3. **Presentation doc changes are suggestions.** At the end of every round, update the doc with suggested edits only (suggestion mode), so nothing replaces the approved text until the owner accepts it.
4. **Log every work round in the workspace.** Append the conversation to `turns`: the owner's message verbatim (`role: "me"`), then a short summary of the reply (`role: "claude"`, with `steps`). Check `turns` for `queued` messages and `decisions` for answered ones at the start of every round.
5. Keep the base look: teal brand, coral CTA, Rubik font, light and dark themes.
