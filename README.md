![alt text](<_ (5).jpeg>)
# Lab 2 – Git & GitHub (Branches, Stash, Pull, Tags)

| # | Command | Definition |
|---|---------|------------|
| 1 | `git init` | Turns the `Lab2git` folder into a Git repository by creating the hidden `.git` folder. |
| 2 | `git remote add origin git@github.com:3lyanz/lab2git-github.git` | Links the local repo to the GitHub repo over SSH and names that remote `origin`. |
| 3 | `git branch -M main` | Renames the current branch to `main`. `-M` forces the rename even if `main` already exists. |
| 4 | `git add .` | Stages all new and changed files in the folder (here, `index.html`). |
| 5 | `git commit -m "commit 1"` | Creates the first (root) commit with the staged files. |
| 6 | `git branch` | Lists local branches. The `*` marks the branch you're on. |
| 7 | `git push -u origin main` | Uploads `main` to GitHub. `-u` sets `origin/main` as its upstream, so later `git push`/`git pull` work without arguments. |
| 8 | `git switch -c dev` | Creates a new branch `dev` from the current commit and switches to it. |
| 9 | `git log` | Shows the commit history: hash, author, date and message. `HEAD -> dev` shows which branch you're on. |
| 10 | `git switch main` | Switches back to the existing `main` branch. |
| 11 | `git switch -c test` | Creates a new branch `test` from `main` and switches to it. |
| 12 | `git switch dev` | Switches to the `dev` branch. |
| 13 | `git push -u origin dev` | Publishes the `dev` branch to GitHub and sets its upstream. |
| 14 | `git push -u origin test` | Publishes the `test` branch to GitHub and sets its upstream. |
| 15 | `git add .` → `git commit -m "commit 1 dev"` | Stages and commits a change on the `dev` branch only. |
| 16 | `git push -u origin dev` | Pushes the new `dev` commit to GitHub. |
| 17 | `git switch test` → `git add .` → `git commit -m "commit 1 test"` | Switches to `test`, then stages and commits a change on it. |
| 18 | `git push -u origin test` | Pushes the new `test` commit to GitHub. |
| 19 | `git switch main` | Switches back to `main`. |
| 20 | `git pull origin main` | Downloads new commits from GitHub's `main` (made on the website) and merges them into local `main`. Here it was a fast-forward. |
| 21 | `git branch -d test` | Deletes the local `test` branch. `-d` refuses if the branch has unmerged work. Use `-D` to force. |
| 22 | `git push origin --delete test` | Deletes the `test` branch from GitHub. |
| 23 | `git switch dev` | Switches to `dev` to continue working there. |
| 24 | `git stash -m "work in progress"` | Saves uncommitted changes to a temporary stash with a label and cleans the working directory, so you can switch branches safely. |
| 25 | `git switch main` → `git add .` → `git commit -m "removed comma"` | Goes to `main` to make a quick fix and commits it. |
| 26 | `git push -u origin main` | Pushes the fix to GitHub's `main`. |
| 27 | `git switch dev` | Returns to `dev`. |
| 28 | `git stash pop` | Re-applies the most recently stashed changes and removes them from the stash list. |
| 29 | `git add .` → `git commit -m "added 2 paragraphs"` | Commits the restored work on `dev`. |
| 30 | `git push -u origin dev` ❌ | **Rejected (non-fast-forward).** The remote `dev` had a commit (made on GitHub) that the local `dev` didn't have, so Git refused to overwrite it. |
| 31 | `git stash -m "forgotten pull"` | Tried to stash first. Output was "No local changes to save" because everything was already committed. |
| 32 | `git pull origin dev` ❌ | **Failed: divergent branches.** Local and remote `dev` each had a different new commit, and Git needs you to choose merge or rebase. |
| 33 | `git pull --rebase origin dev` | Downloads the remote `dev` commits, then replays your local commit on top of them. This gives a straight history with no merge commit. |
| 34 | `git push -u origin dev` | Push now succeeds because local `dev` contains everything on the remote plus your commit. |
| 35 | `git switch main` | Switches to `main`. |
| 36 | `git tag v1.7` | Creates a lightweight tag `v1.7` pointing at the current commit, used to mark a version or release. |
| 37 | `git push origin v1.7` | Uploads the tag to GitHub. Tags are not pushed by a normal `git push`. |
| 38 | `git tag` | Lists all local tags. |
| 39 | `git tag -d v1.7` | Deletes the tag locally. |
| 40 | `git push origin --delete v1.7` | Deletes the tag from GitHub. |
| 41 | `touch README.md` | Creates an empty README file. It isn't tracked until you `git add` and commit it. |

**Notes**
- Instead of `git pull --rebase`, `git pull --no-rebase origin dev` would also work. It merges the two histories and creates a merge commit.
- To avoid the "divergent branches" prompt every time, set a default once: `git config --global pull.rebase true` (or `false` for merge).