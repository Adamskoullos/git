# Quick Guide To Git Workflows

- [Basic Commands](#Basic-Commands)
- [Save local feature changes and update from dev branch](#Save-local-feature-changes-and-update-from-dev-branch)

---

## Basic Commands

- `git log -1` > Get last commit
- `git revert (id)` > Reverts back to a previous commit
- `git branch -D branchName` > Delete local branch after mergin with development
- `git push origin branchName` > push code to separate feature/hotfix branch before creating a pull request to development. This creates the branch if it does not already exist

---

## Stash local feature changes and update from dev branch

Dev branch has been updated and the feature branch needs to update to reflect these:

1. Save any un committed changes on local feature branch: `git stash`
2. Get back into local dev branch: `git fetch && git checkout development`
3. Pull changes from origin to update local dev branch: `git pull`
4. Get back into local feature branch: `git fetch && git checkout featureBranch`
5. Merge updated local dev branch into feature branch: `git merge development`
6. Now the feature branch is updated, carry on by first reinstating stashed changes: `git stash apply`

---
