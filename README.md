# Digital Knowledge Management System

A personal knowledge vault built on the zettelkasten method.

## Layout

```
journals/    Daily notes. The inbox for fleeting notes (Logseq journals)
pages/       All lasting notes. Flat — classification comes from links and
             the type:: property, not from folders
templates/   Note templates (for the Obsidian Templates plugin)
assets/      Images and other attachments
logseq/      Logseq configuration
```

## Opening it

- **Logseq**: Add new graph → select this folder
- **Obsidian**: Open folder as vault → select this folder

Both apps read the same files, so **do not keep them open and editing at the same time.**

## Conventions

Note kind is carried by the `type::` property: `fleeting` / `literature` / `permanent` / `structure`.
Full rules in `pages/Zettelkasten Operating Rules.md`.

Sync commands are in `git-cheatsheet.md`.
