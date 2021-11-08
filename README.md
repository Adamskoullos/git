# Quick Guide To Git Workflows

A reference guide for more intermediate daily workflows in Git.

- [Basic Commands](#Basic-Commands)
- [Clone dev branch for feature or hotfix](#Clone-dev-branch-for-feature-or-hotfix)
- [Stash local feature changes and update from dev branch](#Stash-local-feature-changes-and-update-from-dev-branch)
- [Rebase](#Rebase)
- [Handling merge conflicts](#Handling-merge-conflicts)

---

## Basic Commands

- `git log` > To see a list of commits. Can grab commit id if needed for revert
- `git log -1` > Get last commit
- `git revert (id)` > Reverts back to a previous commit
- `git branch -D branchName` > Delete local branch after merging with development
- `git push origin branchName` > Push code to separate feature/hotfix branch before creating a pull request to development. This creates the branch if it does not already exist
- `git reset HEAD fileName` > Unstage a file before committing changes. Do this to only have changes relevant to message. Later re-add the file by using `git add fileName` or just `git add .`

---

## Clone dev branch for feature or hotfix

1. Clone repo onto local machine: `git clone (url)`
2. `cd` into repo and `git branch` to confirm what branch we are on
3. Create a new branch and switch into it: `git checkout -b newBranch`

When ready to commit code:

4. Confirm branch and changes with `git status`, then commit to local feature branch and then push up to origin feature branch:

   - `git add .`
   - `git commit -m "message"`
   - `git push origin branchName` > This adds to feature/hotfix branch or makes a new one if it does not exist

5. When finished create a pull request into development

---

## Stash local feature changes and update from dev branch

Dev branch has been updated and the feature branch needs to update to reflect these:

1. Save any un committed changes on local feature branch: `git stash`
2. Get back into local dev branch: `git fetch && git checkout development`
3. Pull changes from origin to update local dev branch: `git pull`
4. Get back into local feature branch: `git fetch && git checkout featureBranch`
5. Merge updated local dev branch into feature branch: `git merge development`
6. Now the feature branch is updated, carry on by first reinstating stashed changes: `git stash apply`

Another way to update a feature branch if there has been changes made to development since the branch, is to use `rebase`

---

## Rebase

If the development branch has changed since the initial feature/hotfix branch we can update the branch by adding the changes from development as if they were already there before we started making changes in the feature branch:

1. get into development and pull any updates from origin: `git checkout development`, `git pull origin development`
1. Once local development is up to date, get into feature branch: `git checkout featureBranch`
1. Grab all changes to development and update the feature branch, placing any feature branch changes after the changes from development:
   `git rebase development`

Now any updates from the development branch have been added to the feature branch, before any feature branch commits.

---

## Handling merge conflicts

Lets say two devs are working on the same feature branch:

If pushing to an origin branch (feature or hotfix) causes merge conflicts we can kill two birds with one stone by syncing with the origin branch as well as adding our changes back to our local branch with one command: `pit pull origin branchName --rebase`

At this point our local branch has been updated with the origin branch and our local changes have been re-added to the local branch. Its now time time to push the local branch back to the origin branch: `git push origin branchName`
