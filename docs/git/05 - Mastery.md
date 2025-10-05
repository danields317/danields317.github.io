# Git Mastering Techniques
## 4 areas
1. Working area. The local directory where work is done.
2. Repository. The Git database with all commits and branches.
3. Index. The area where files that will be put in a commit live (staging).
4. Stash. Temporary storage area.
## Removing files
`git remove <filename> --cached`
Removes the file from the staging area.
## Renaming files
When a file is renamed, it practically means that the initial file is removed and a new file is created. Both the 'new' file and the 'removed' file need to be added to the staging area. Most of the time Git is smart enough to notice that the file was actually renamed because the content is the exact same (or very similar).
# Git Reset
The reset command gives the option to make a branch point to a different commit.
`git reset <commit-hash>`
Git reset has 2 common options:
**--hard**
Will reset the branch to the chosen commit and copies the content to the project folder. Used when new commits are actually unwanted and you want to go back to a previous version of the project entirely.
**--mixed (default)**
Will reset the branch to the chosen commit and unstages all changes made. The changes will still be in the project folder, but have to staged again.
# Stashing
Stash is a way to store changes without creating a commit and putting it in the repository.
`git stash`
Stashes the changes that are in the working area and not in the current commit. Then resets the working area to that commit.
`git stash apply`
Grabs the stashed information and puts it back in the working area.
# Path checkout
`git checkout HEAD <path>`
When performing checkout with a path, only that path or file is changed to its state in the specified commit. It does not change the head. This can be dangerous since changes are lost.
# Commit part of file
`git add --patch <file>`
This opens an interactive system to decide which parts of the file should be committed. File is split up in 'hunks' and you can choose which parts to stage and which not.
# History
`git log --graph --decorate --online`
Gives a 'pretty' overview of the project history in the terminal.
`git show HEAD^` and `git show HEAD~1`
Shows commit before commit head is pointing at
`git blame <file-path>`
Tells which line was changed in which commit by who.
`git diff <commit 1> <commit 2>`
shows differences between commits (can also be used for branches)