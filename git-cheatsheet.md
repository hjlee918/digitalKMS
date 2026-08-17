# Git Sync Cheatsheet — DKMS

Commands for syncing this vault with GitHub (`hjlee918/digitalKMS`).

> No `#` comments inside the code blocks. Interactive zsh reads `#` as a command and errors out, so blocks are safe to paste whole.

---

## 0. The concept — why several commands

Git has three stages. Understand this and the rest follows.

```
working folder  →  staging  →  local repo  →  GitHub
                add        commit        push
```

Editing a file does not record anything. You **select (add) → confirm (commit) → upload (push).** Three separate actions.

---

## 1. Daily flow — pushing up

After writing notes:

```bash
cd "/Users/johnlee/Digitial Knowledge Management System"
git add -A
git commit -m "Add note: cognitive load"
git push
```

- `-A` — everything that changed
- `-m` message — this is a note to your future self. Write **what changed**, not "update".

---

## 2. Before you start — pulling down

If anything was edited elsewhere (Claude on web/mobile, or GitHub's web editor), pull **before** you start working on the Mac.

```bash
cd "/Users/johnlee/Digitial Knowledge Management System"
git pull --rebase
```

`--rebase` avoids pointless "Merge branch..." commits and keeps history readable. Better for a single-user note repo.

> **One habit covers most of it: pull when you open, push when you close.**
> Most conflicts come from skipping this.

---

## 3. Checking state

| Command | When to use it |
|---|---|
| `git status` | First thing to type when confused. What changed, what is staged |
| `git log --oneline -10` | Last 10 commits. Skim what you have been doing |
| `git diff` | Line-by-line view of unstaged changes. Review before committing |
| `git diff --staged` | View what is already staged. Final check before commit |

---

## 4. Undoing things

Fix a bad commit message (before pushing):

```bash
git commit --amend -m "A proper message"
```

Restore one file to its last committed state:

```bash
git checkout -- "pages/Note Name.md"
```

Remove untracked new files — preview first, then execute:

```bash
git clean -nd
```

```bash
git clean -fd
```

> ⚠️ `git clean -fd` deletes uncommitted new files **unrecoverably.**
> Always run `-nd` (dry run) first to see what would go.

---

## 5. When a conflict happens

If `git pull --rebase` hits the same line edited on both sides, it stops:

```
CONFLICT (content): Merge conflict in pages/Note.md
```

Open the file and you will find markers:

```
<<<<<<< HEAD
what was on the remote
=======
what you wrote
>>>>>>> your commit
```

Edit it into the form you want, delete the `<<<`, `===`, `>>>` lines, then:

```bash
git add -A
git rebase --continue
```

To give up and go back to where you started:

```bash
git rebase --abort
```

---

## 6. Making it easier (later)

Add to the bottom of `~/.zshrc`:

```bash
alias dkms='cd "/Users/johnlee/Digitial Knowledge Management System"'
alias dkpull='cd "/Users/johnlee/Digitial Knowledge Management System" && git pull --rebase'
alias dkpush='cd "/Users/johnlee/Digitial Knowledge Management System" && git add -A && git commit -m "sync: $(date +%Y-%m-%d\ %H:%M)" && git push'
```

Run `source ~/.zshrc` once and `dkpush` does the whole thing.

> **Do not use aliases for the first two or three weeks.**
> Automating before `git status` becomes reflex leaves you helpless when something tangles.

---

## 7. Practice sequence

1. Create a note → `git status` → add / commit / push → confirm it on GitHub in the browser
2. Edit a file directly on GitHub's web editor → `git pull --rebase` on the Mac → confirm it landed
3. Deliberately create a conflict (edit the same line on both sides) → resolve it

Get through step 3 and most of the anxiety about git disappears.

---

## 8. Constraints specific to this vault

- **Run git only in the Mac terminal.** Running it through Claude's folder bridge leaves a stale `.git/index.lock` and produces "Another git process seems to be running". Clear it with `rm -f .git/index.lock`.
- **Never let git and iCloud/Drive sync the same folder.** Concurrent syncing corrupts `.git`. Pick one sync mechanism.
- The repo is **public**, so reads need no auth but **pushes still do.** Pushing from a cloud session requires a fine-grained PAT.
- Files matched by `.gitignore` never upload, no matter how often you run `git add -A`. If something refuses to appear, check `.gitignore` first.

---

## Quick reference

```
opening     git pull --rebase
closing     git add -A  →  git commit -m "..."  →  git push
stuck       git status
```
