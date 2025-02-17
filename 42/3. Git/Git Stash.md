- allows you to temporarily save changes without commiting
- can switch to another branch 
- stashes are not tied to the lifespan of your IDE or any specific session; they are part of the Git repository and will persist until you choose to remove them.

# Commands
`git stash`
	`push <name>` - saves stash with a name
	`list` - lists all stashes created, shows the index
	`apply` - apply latest stash
	`pop` - apply latest stash, then removes it from stash list
	`clear` - delete all stashes
	`show stash@{stash-index}` - shows changes in specified stash
	`show -p stash@{stash-index}` - shows the full diff
	`apply stash@{stash-index}` - applies specific stash
	`drop stash@{stash-index}` - deletes specific stash
	`-u` - track unchanged files
	`-a` - stash all changes including untracked and ignored files

## Use case to stash specific file changes
	`push "<name>" file1.txt`
	`apply stash@{stash-index} -- file1.txt`

# Best Practices
- Stash changes before pulling or switching to avoid conflicts
- Descriptive stash messages
- Before applying or popping a stash, use `show` to review
- Regularly remove unused stash