## makes it possible to checkout multiple branches of the SAME repository 

## Run the command in the repo you want
`git worktree list` - shows available worktrees

`git worktree add {directory} {active-repo-branch}` - adds the branch
{directory} = ~/.worktree/{file-name}
(typical practice) 

## Then cd into the directory and open IDE from there

`git worktree remove {directory}` - deletes the worktree 
