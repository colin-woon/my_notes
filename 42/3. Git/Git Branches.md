# `HEAD` - a pointer that points to the latest commit on the working branch
# Take note for delete: If you deleted a remote branch, you should also delete its tracking local branch, prevents obsolete branches.
# How to merge/rebase:
```
git switch {destination-branch}
git merge/rebase {source-branch} //merge commit message will be required
```

# Difference between merge and rebase IMPORTANT
- Merge will combine all commit history between two branches
- Rebase will append the local commit history on top of the source/remote commit history
## When to use rebase
- to clean up your local commit, usually before you merge into a team branch, you rebase the original codebase in case there are any changes
- DO NOT REBASE pushed commits on remote repo, it will affect other developers as it rewrites commit history, some references will not have the same id anymore

# Commands
`git branch` - list branches
	`{branch-name}` (creates new branch)
	`-d {branch-name}` (deletes local branch, **-D for force delete**) 
	`-m {new-branch-name}` (renames current branch)
	`-m {other-branch} {new-name}` (renames other branch, not active)
	`--track {new-local-branch} origin/{remote-branch}` (fetches a remote branch locally)
	`-v` (additional info)

`git checkout/switch <branch-name>` - switch branches
	`-b` (create and switch branch)
	`-- {file-name}` (discard file changes)
	`--track origin/{remote-branch}` (same as git branch --track, but autonames local branch with remote-branch name)
	`-` - goes back to previous branch, make sure no branch name

`git fetch <remote>/--all`  - retrieves changes from a remote repo without merging

`git pull <remote> <branch>` - git fetch but with merging
	`--rebase` (appends commit history at bottom of local branch, hence why its called re-base)

`git push -u <remote> <branch>` - sets upstream branch, linking local branch to remote branch 
	`git push origin --delete <branch-name>` (deletes remote branch)

`git log <source-branch>../...<comparing-branch>` - sees difference between commits, if `..` only, shows what commits are in comparing branch that are not in source branch. if `...`, shows both.

`git commit` 
	`-am` - adds add changes and commits in one go
	`--amend -m` - changes last commit message
	`--amend --no-edit` - commits files only to last commit without changing commit message 

`git config --global alias.<alias-name> "<git-command>"` - creates an alias for git commands

`git revert <commit-hash>` - creates a new commit that undoes changes based in the reverted commit
	If `<commit-hash>` is HEAD, reverts last commit.
	Maintains commit history

`git reset <option-below> <commit-hash>` - if without anything, it will reset staging area, usually used to undo commits or unstage changes
	`--hard` - discard changes in working and staging, 

 `git push origin --delete <branch-name>` 
# Merge Conflicts
`git merge --abort` - cancels the merge
If there is a conflict, once it is fixed, need to git add and commit again. 

# Squashing
- Used to combine multiple consecutive commits into a single commit on the feature/bug branch before merging with staging/production branch.
`git rebase`
	`-i` - interactive mode, will jump into text editor
	`<commit-hash>` - the commit just before the first one that you want to squash 
	OR
	`HEAD~<number-of-commits>` - from the last commit to the specified number of commits that you want to squash
	OR
	`--autosquash` - only can be done if your commits have the `--squash` flag
```
//THEN
pick abc123 First commit //pick should always be the first commit
squash def456 Second commit
squash xyz789 Third commit

//THEN ANOTHER EDITOR WILL OPEN TO MODIFY THE COMMIT MESSAGES IF REQUIRED
```
```--continue``` - proceed with rebase

# Cherry-pick
`git cherry-pick <commit-hash-from-source-branch>` - creates a new commit based on a specific commit in the current active branch. make sure branch has been switched.
