---
name: rehearsal-git-sync
description: Sync, commit, and push the /tmp/Rehearsal Git repository to GitHub over SSH (git@github.com:ShengNW/Rehearsal.git). Use when asked to push/sync this repo, update .gitignore to ignore CodexDev/, repair the origin remote, or ensure main tracks origin/main.
---

# Rehearsal Git Sync

## Overview

Commit local changes in /tmp/Rehearsal and push them to the GitHub repo via SSH while keeping CodexDev ignored.

## Workflow

### 1. Confirm repository

- Run `pwd` and `git rev-parse --show-toplevel`; if not `/tmp/Rehearsal`, `cd /tmp/Rehearsal`.
- If `.git` is missing, stop and report that the repository is not initialized.

### 2. Enforce CodexDev ignore

- Ensure `.gitignore` exists and contains `CodexDev/` on its own line. Append if missing.
- If `CodexDev` is already tracked, remove it from the index with `git rm -r --cached CodexDev` (do not delete local files).

### 3. Verify remote and branch

- Check `git remote get-url origin`; if missing or HTTPS, set:
  `git remote add origin git@github.com:ShengNW/Rehearsal.git` or `git remote set-url origin git@github.com:ShengNW/Rehearsal.git`.
- Ensure the current branch is `main`; if not, run `git branch -M main`.

### 4. Stage and commit

- Run `git status -sb` and `git add .`.
- If there are staged changes, choose a concise commit message from the user request; if none provided, use `Update`.
- Run `git commit -m "<message>"`.
- If the working tree is clean, skip the commit step and continue to push.

### 5. Push

- If upstream is missing, push with `git push -u origin main`.
- Otherwise run `git push`.
- Report the push result and final `git status -sb` summary.
