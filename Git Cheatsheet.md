This is a list of commands and tips to use git. For info on getting started visit [Introduction to git](Introduction%20to%20git#download%20git)

## Basic Git Commands
*`git add`*
- Adds files specified to the *staging* area
- Most common use is `git add -A` which adds all applicable files.

*`git commit`*
- commits all staged files/changes to the *local repository*
- Best practice is to provide a message so people know the purpose of the commit with the `-m` flag
- Ex. `git commit -m "This is a commit message"`

*`git push`*
- Pushes all local commits to the remote repository
- Don't commonly include flags

*`git pull`*
- Merges the remote repository into your local repository
- Technically it's doing a `git fetch` and `git merge`, but you don't need to worry about that unless your local branch and the remote repository's branch don't have the same commits

*`git status`*
- displays information such as the current branch you are on, if it's up to date with origin (may still not be updated with the remote repository, do a `git fetch` or `git pull` to check)
- Displays a list of staged files/changes (useful to see if your files are being added correctly)

*`git branch`*
- Lists the different branches on your local repository
- The `-D` flag will delete a local branch
- The `-A` flag will include remote branches in the list
- The `-m` flag will let you rename the branch
- Using no parameters but just text will create a new branch
	- Ex. `git branch branch-name`

*`git checkout`*
- Allows you to check out an already created branch
- Creates a new local branch with the *upstream* set as the remote version of said branch if a branch with that name exists on origin
- Ex. `git checkout branch-name`
