type:: structure
created:: 2026-08-17
tags:: meta, MOC

## Division of labour
Several tools look at this one folder. The source of truth is always **the markdown files themselves** — no app is authoritative.

- **Logseq** — daily writing. Catches fleeting notes in the journal and works them block by block. It is the opinionated one, requiring `journals/` and `pages/`, so the folder layout follows Logseq's expectations.
- **Obsidian** — opens the same folder. Used for **reading and auditing** via graph view and Dataview. Writing is better done in Logseq; fewer collisions.
- **GitHub** — storage and transport. The only route to these notes when the Mac is off.
- **Notion** — not file-based, so it lives outside this vault. Use it as an exit: a place to move finished work meant for other people.
- **Roam** — experimental. Not synced with this vault. If something needs to move, do a one-off markdown or JSON export.

## Cautions
- Git and iCloud/Drive syncing the same folder will corrupt `.git`. Use exactly one sync mechanism.
- Run git commands in the Mac terminal only.
- Do not keep Logseq and Obsidian open on this folder at the same time.

## Links
- Parent: [[000 Index]]
- Method: [[Zettelkasten Operating Rules]]
