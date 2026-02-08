# Fundamentals

When creating a project, files with code are placed in a folder. When putting this project under version management with Git, Git creates a repository somewhere else. In this repository, snapshots of the project are saved. When moving between snapshots, branches, etc. You tell Git to grab something out of the repository and place it in the project folder or vice versa.

![Git](/img/git/git-overview.png)

## Project initialization

`git init`
Initializes a repository for a project tracked through GIT. Creates a .git folder inside of the root where git stores its information for tracking the project. The snapshots of the project will be stored in this repository.

## Staging

`git add <filename>` for one file or `git add -A` for all files
Adding files to the staging area tells Git that these files should be added in the next commit.

## Commits

`git commit -m "<message>"`
Creates a Git commit. A commit is a snapshot in the project that saves the state of the project at that time. Meaning that the state of the project at that time can be restored. The commit sends the staged files to the repository where it is saves. Commits have a unique hash as their ID.

## Checkout

`git checkout <commit id>`
Grabs a commit from the repository and places it in the project folder. Giving the ability to check out previous versions of the project.

## Branching

`git branch <branch name>`
With branching, different versions of a project can be developed besides each other. Branches are mostly used to develop one new feature that then will be merged into the main one.
`git switch <branch name>`
Switch over to other branch
`git merge <branch to merge into current>`
Merges another branch into current branch to contain all code from other branch.

## Distributed version control

By saving the repository on a server, multiple people can access it and work together on a project. But to work on it, the project does need to be cloned to the local machine.
`git clone <url>`
Clones the repository from the server to local machine.
`git pull`
Pulls the information in the remote repository to the local repository.
`git push`
Pushes information from the local repository to the remote repository.
