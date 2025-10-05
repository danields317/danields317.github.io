# Distributed Version Control
Until now, all documentation is about how Git operates on one machine. The real power of Git is being able to share code easily. This is done through Git's distribution features.
## Origin
When cloning a remote repository, the entire .git database is copied.
When cloning a repository, .git/config file will add information about the remote repository. This information is labelled with the name origin.

When cloning, only the main branch is cloned by default.

The origin branches are just locally stored branches that have the same information as the branches on the remote. When using `git fetch` the locally stored remote branches get synchronized with their remote counterparts. These branches can be seen as read only. To work on a branch that was fetched from the remote, a local copy of the branch is created.
  
Git remembers that the local branch is a copy of the remote branch. So when pushing, Git knows which branch should now point to a new commit.

When a remote branch gets updated from another source than the local repository (e.g. another developer pushed to your working branch), the local remote branch can be updated with `git fetch`.

After fetching, the working branch can merge the local remote branch and create a new commit. This can then be pushed to the remote so all changes from the remote and the local changes are properly placed.

![Config](/img/git/config-overview.png)

Rebasing should not be done when a commit has already been shared with the remote since it is not really possible to fix.