# Project Nova: Troubleshooting & Emergency Fixes

Part 2 of the Git Mastery & Troubleshooting Activity (CS223).

## 1. The "Oops, wrong file" Problem
- **Problem:** `git add .` accidentally staged `.env`, which contains sensitive database passwords.
- **Solution:** Unstage the specific file while keeping local changes intact.
- **Command:** `git restore --staged .env` (or `git reset HEAD .env`)

## 2. The "Typo in the message" Problem
- **Problem:** "authentication" was misspelled as "authnetication" in the latest commit message, and nothing has been pushed yet.
- **Solution:** Modify the most recent commit message without creating a new commit.
- **Command:** `git commit --amend -m "Fixed authentication typo"`

## 3. The "Forgot a file" Problem
- **Problem:** A commit was made, but `styles.css` was forgotten and belongs with that exact commit.
- **Solution:** Stage the forgotten file, then merge it into the previous commit without changing the message.
- **Command:**
  1. `git add styles.css`
  2. `git commit --amend --no-edit`

## 4. The "I hate these changes" Problem
- **Problem:** `index.html` is completely broken after an hour of experimenting, and nothing is staged or committed.
- **Solution:** Discard all local changes for that file.
- **Command:** `git restore index.html` (or `git checkout -- index.html`)

## 5. The "Wrong Branch" Problem
- **Problem:** Three commits were made on `main` instead of a feature branch, and nothing has been pushed yet.
- **Solution:** Create a new branch pointing to these commits, then roll `main` back by 3 commits.
- **Command:**
  1. `git branch new-feature`
  2. `git reset HEAD~3 --hard`
  3. `git checkout new-feature`

## 6. The "Detached HEAD" Problem
- **Problem:** Commits were made after `git checkout <old-commit-hash>`, and they will be lost when switching back to `main`.
- **Solution:** Create a new branch right where HEAD is to save those floating commits.
- **Command:** `git switch -c recovery-branch` (or `git checkout -b recovery-branch`)

## 7. The "Undo a pushed mistake" Problem
- **Problem:** A bug was committed and pushed to the shared repository, so `git reset` can't safely be used.
- **Solution:** Create a new commit that does the exact opposite of the buggy commit, keeping the timeline intact.
- **Command:** `git revert <buggy-commit-hash>`

## 8. The "Accidental Deletion" Problem
- **Problem:** The wrong branch was deleted with `git branch -d feature-x`, and it still had unmerged work.
- **Solution:** Find the branch's last commit hash with `git reflog`, then recreate the branch.
- **Command:** `git branch <deleted-branch-name> <commit-hash>`

## 9. The "Ghost Files" Problem
- **Problem:** Files were deleted using the file explorer, and Git shows them as deleted under "Changes not staged for commit."
- **Solution:** Tell Git to record the deletions and stage them for the next commit.
- **Command:** `git add -u` (or `git rm <filename>`)

## 10. The "Pushed to the void" Problem
- **Problem:** A branch called `testing-junk` was accidentally pushed to the remote GitHub repository.
- **Solution:** Delete the remote branch directly from the terminal.
- **Command:** `git push origin --delete testing-junk`
