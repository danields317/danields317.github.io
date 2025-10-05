# Commit message standards
Commit messages are an important feature to understand the changes the commit makes. A (not official, but commonly) standard exists to make writing and reading commit messages easier.
## Base layout
```git
<Type>(<scope>): <description>

<optional body>

<optional footer>
```
# Merge Commit
When commiting the result of a merge of two branches, enter the branch that was merged into the working branch.
```git
Merge branch "<branch name>"
```
<sup>Follows default git merge message</sup>
# Revert Commit
```git
Revert "<reverted commit subject line>"
```

# Initial Commit 
```git
init
```

## Types
* API relevant changes.
    * `feat` Commits, that adds or remove a new feature.
    * `fix` Commits, that fixes a bug.
* `refactor` Commits, that rewrite/restructure your code, however does not change any API behavior.
    * `perf` Commits are special `refactor` commits, that improve performance.
* `style` Commits, that do not affect the meaning (white-space, formatting, missing semi-colons, etc.).
* `test` Commits, that add missing tests or correcting existing tests.
* `docs` Commits, that affect documentation only.
* `build` Commits, that affect build components like build tool, ci pipeline, dependencies, project version, etc.
* `ops` Commits, that affect operational components like infrastructure, deployment, backup, recovery, etc.
* `chore` Miscellaneous commits e.g. modifying `.gitignore`.
## Scopes
The `scope` provides additional contextual information.
* Is an **optional** part of the format.
* Allowed Scopes depends on the specific project.
* Using ticket/issue ID's as scope is seen as a bad practice since it causes dependency on ticketing tools (e.g. Jira).
## Breaking Changes Indicator
Breaking changes should be indicated by an `!` before the `:` in the subject line e.g. `feat(api)!: remove status endpoint`.
* Is an **optional** part of the format.
## Description
The `description` contains a concise description of the change.
* Is a **mandatory** part of the format.
* Use the imperative, present tense: "change" not "changed" nor "changes".
  * Think of `This commit will...` or `This commit should...`.
* Don't capitalize the first letter.
* No dot (`.`) at the end.
## Body
The `body` should include the motivation for the change and contrast this with previous behavior.
* Is an **optional** part of the format.
* Use the imperative, present tense: "change" not "changed" nor "changes".
* This is the place to mention issue identifiers and their relations.
## Footer
The `footer` should contain any information about **Breaking Changes** and is also the place to **reference Issues** that this commit refers to.
* Is an **optional** part of the format.
* **optionally** reference an issue by its id.
* **Breaking Changes** should start with the word `BREAKING CHANGES:` followed by space or two newlines. The rest of the commit message is then used for this.