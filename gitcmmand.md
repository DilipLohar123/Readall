# Git Commands Cheat Sheet

A collection of essential Git commands with simple examples.

## 1. Initialize a Repository
```
git init
```
Initializes a new Git repository in the current folder.

## 2. Clone a Repository
```
git clone <repository-url>
```
Downloads a repository from a remote source.

## 3. Check Status
```
git status
```
Shows the status of changes as untracked, modified, or staged.

## 4. Add Files to Staging
```
git add <file>
```
Adds a file to the staging area.

```
git add .
```
Adds all files to the staging area.

## 5. Commit Changes
```
git commit -m "Your message"
```
Records the staged changes to the repository.

## 6. View Commit History
```
git log
```
Shows the commit history for the current branch.

## 7. Push Changes
```
git push origin <branch>
```
Uploads local branch commits to the remote repository.

## 8. Pull Changes
```
git pull
```
Fetches and merges changes from the remote repository.

## 9. Create a New Branch
```
git branch <branch-name>
```
Creates a new branch.

## 10. Switch Branches
```
git checkout <branch-name>
```
Switches to the specified branch.

## 11. Merge Branches
```
git merge <branch-name>
```
Merges the specified branch into the current branch.

## 12. Delete a Branch
```
git branch -d <branch-name>
```
Deletes the specified branch.

## 13. Stash Changes
```
git stash
```
Temporarily saves changes that are not ready to commit.

## 14. Apply Stashed Changes
```
git stash apply
```
Applies the most recently stashed changes.

## 15. View Remote URLs
```
git remote -v
```
Shows the URLs of remote repositories.

## 16. Add a Remote
```
git remote add origin <url>
```
Adds a new remote repository.

## 17. Remove a Remote
```
git remote remove origin
```
Removes a remote repository.

## 18. Show Differences
```
git diff
```
Shows the changes between commits, commit and working tree, etc.

## 19. Discard Local Changes
```
git checkout -- <file>
```
Restores a file in the working directory to the last committed state.

## 20. Reset to Last Commit
```
git reset --hard
```
Resets the working directory and staging area to the last commit.

---
_Use these commands as a quick reference for your daily Git workflow!_
