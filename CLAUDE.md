# Talent – working rules

Talent is a Hebrew (RTL) marketplace app prototype in a single file, `index.html`. Two user types: talents (כישרונות) offer services; scouts (סקאוטים) browse, like, save and book.

## Where things live

- Workspace (the owner's home for the project): https://claude.ai/artifact/9Gs5fhgSFLphixd31ZoY1H
  - Its database has `ideas` (the ideas chat, plus work conversations) and `app` (`current` = approved app version, `pending` = waiting for approval, `previous`).
- Published app page: https://claude.ai/artifact/KyPhBFZcPWFohzmJa9fDmL (publish updates from `index.html` to this URL).
- Presentation doc (Claude Docs): https://claude.ai/artifact/Y1dY32SyxKXpLLzhjkU2XB

## Rules from the owner

1. **Don't guess.** When a request can be read more than one way, send two options and let the owner pick. If neither fits, they correct that topic.
2. **App versions need approval.** After code changes: commit and push, publish the app page, then write `app/pending` in the workspace database (`url`, `title`, `notes`, `publishedAt`). The owner approves or rejects with the buttons in the workspace. Never write `app/current` yourself unless the owner says the version is approved.
3. **Presentation doc changes are suggestions.** At the end of every round, update the doc with suggested edits only (suggestion mode), so nothing replaces the approved text until the owner accepts it.
4. **Log every work round in the workspace.** Append the conversation to `ideas`: a `sep` entry for the session, then `chat` entries with the owner's message verbatim in `text` and a short summary of the reply in `reply`.
5. Keep the base look: teal brand, coral CTA, Rubik font, light and dark themes.
