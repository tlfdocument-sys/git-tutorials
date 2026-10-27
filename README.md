just learning

# Complete Git Commands Cheat Sheet

Beginner to Advanced • Windows PowerShell • VS Code • GitHub • Azure DevOps

This is your practical Git reference guide, organized by task. For every important command, you'll learn what it does, why you need it, how to use it, and when to use it.

All examples use PowerShell and your practice repository:

```
C:\Users\LENOVO\git-tutorial\lesson-01
```

PowerShell rule: Type the command itself, not the `$` prompt shown in Linux tutorials.

## 1. Git command workflow at a glance

Working directory

Create or modify files

`git status` · `git diff`

Staging area

Choose changes for the next commit

`git add` · `git diff --cached`

Local repository

Save and inspect project history

`git commit` · `git log`

Remote repository

Collaborate with your team

`git fetch` · `git pull` · `git push`

## 2. Installation and configuration

| Command                                            | Why / when to use it                                             |
| -------------------------------------------------- | ---------------------------------------------------------------- |
| `git --version`                                    | Check the installed Git version.                                 |
| `git config --list`                                | Inspect effective Git configuration.                             |
| `git config --global --list`                       | Inspect your user-level configuration.                           |
| `git config --global user.name "Your Name"`        | Set the author name recorded in your commits.                    |
| `git config --global user.email "you@example.com"` | Set the commit author email.                                     |
| `git config --global init.defaultBranch main`      | Make new repositories start with `main`.                         |
| `git config --global core.editor "code --wait"`    | Use VS Code as Git's editor, if the `code` command is available. |
| `git config --show-origin --list`                  | See which configuration file supplied each setting.              |
| `git help <command>`                               | Read help for a particular command. Example: `git help commit`.  |

Example:

```
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
```

When to use: Set your identity and preferred default branch once on your computer. Check your work email and company policy before configuring identity for company commits.

## 3. Create, initialize, and clone repositories

| Command                               | Why / when to use it                                                      |
| ------------------------------------- | ------------------------------------------------------------------------- |
| `git init`                            | Start tracking a project in the current directory.                        |
| `git init -b main`                    | Initialize a repository with `main` as its initial branch.                |
| `git clone <URL>`                     | Download a remote repository and its history.                             |
| `git clone <URL> <folder>`            | Clone into a folder with a chosen name.                                   |
| `git status`                          | See whether the directory is a repository and whether files have changed. |
| `git rev-parse --show-toplevel`       | Find the root of the current Git repository.                              |
| `git rev-parse --is-inside-work-tree` | Check whether you're inside a working tree.                               |
| `git ls-files`                        | List files currently tracked by Git.                                      |

Examples:

```
git init -b main
```

```
git clone https://example.com/organization/project.git
```

The URL above is illustrative; use the real repository URL supplied by your organization.

When to use: Use `git init` for a new local project, and `git clone` when a repository already exists remotely. Don't run `git init` repeatedly inside an existing repository without a reason.

## 4. Everyday file and staging commands

| Command                      | Why / when to use it                                                          |
| ---------------------------- | ----------------------------------------------------------------------------- |
| `git status`                 | Check changes before staging, committing, or switching branches.              |
| `git add hello.txt`          | Stage one specific file.                                                      |
| `git add .`                  | Stage changes under the current directory, including additions and deletions. |
| `git add -A`                 | Stage additions, modifications, and deletions across the working tree.        |
| `git add -p`                 | Interactively select individual change sections to stage.                     |
| `git diff`                   | Review unstaged changes.                                                      |
| `git diff --cached`          | Review changes staged for the next commit.                                    |
| `git diff --stat`            | See a summary of changes.                                                     |
| `git diff --name-only`       | List files changed between compared states.                                   |
| `git rm <file>`              | Remove a tracked file and stage its deletion.                                 |
| `git mv <old> <new>`         | Move or rename a file while updating Git's index.                             |
| `git check-ignore -v <file>` | Identify which `.gitignore` rule ignores a file.                              |

Example workflow:

```
git status
git diff
git add hello.txt
git diff --cached
git status
```

Why review first? It prevents accidentally committing unrelated files, generated files, or sensitive information.

## 5. Commits and history

| Command                           | Why / when to use it                                                                                      |
| --------------------------------- | --------------------------------------------------------------------------------------------------------- |
| `git commit -m "message"`         | Save staged changes as a commit.                                                                          |
| `git commit -am "message"`        | Stage modifications and deletions of tracked files and commit them; does not include new untracked files. |
| `git commit --amend`              | Edit the latest commit message or content.                                                                |
| `git log`                         | Inspect commit history.                                                                                   |
| `git log --oneline`               | Show compact commit history.                                                                              |
| `git log --graph --oneline --all` | Visualize branches and commit history.                                                                    |
| `git log -n 5`                    | Show the latest five commits.                                                                             |
| `git show <commit-id>`            | Inspect a specific commit and its changes.                                                                |
| `git show --stat <commit-id>`     | Summarize files changed in a commit.                                                                      |
| `git diff HEAD~1 HEAD`            | Compare the latest commit with its parent.                                                                |
| `git shortlog -sn`                | Summarize commits by author.                                                                              |
| `git log --since="7 days ago"`    | Filter history by date.                                                                                   |

Example:

```
git add .
git commit -m "Add product validation"
git log --oneline --graph --all
```

Commit message tip: Prefer clear descriptions such as `Add invoice validation` or `Fix inventory calculation` rather than `Changes` or `Update`.

## 6. Branching and merging

| Command                       | Why / when to use it                                                                       |
| ----------------------------- | ------------------------------------------------------------------------------------------ |
| `git branch`                  | List local branches.                                                                       |
| `git branch -a`               | List local and remote-tracking branches.                                                   |
| `git branch -vv`              | Show branches and their upstream tracking information.                                     |
| `git branch <name>`           | Create a branch without switching to it.                                                   |
| `git switch <name>`           | Switch to an existing branch.                                                              |
| `git switch -c feature/login` | Create and switch to a new branch.                                                         |
| `git branch -M main`          | Rename the current branch to `main`, replacing an existing local branch name if necessary. |
| `git merge <branch>`          | Merge another branch into the current branch.                                              |
| `git merge --abort`           | Attempt to cancel an in-progress merge.                                                    |
| `git branch -d <branch>`      | Delete a merged local branch.                                                              |
| `git branch -D <branch>`      | Force-delete a local branch; may discard unmerged work from that branch.                   |

Example feature workflow:

```
git switch main
git switch -c feature/customer-module
# Make and test your changes
git add .
git commit -m "Add customer module"
git switch main
git merge feature/customer-module
```

The merge command above assumes the feature branch is ready to merge locally. In a company repository, use a pull request if that is the required review process.

## 7. Remote repositories: GitHub and Azure Repos

| Command                             | Why / when to use it                                           |
| ----------------------------------- | -------------------------------------------------------------- |
| `git remote -v`                     | View configured remote names and URLs.                         |
| `git remote add origin <URL>`       | Connect a local repository to a remote.                        |
| `git remote set-url origin <URL>`   | Change the URL associated with a remote.                       |
| `git remote show origin`            | Inspect remote details and tracking configuration.             |
| `git fetch origin`                  | Download remote updates without integrating them.              |
| `git fetch --prune origin`          | Fetch updates and remove stale remote-tracking references.     |
| `git pull`                          | Fetch and integrate updates from the configured upstream.      |
| `git pull --rebase`                 | Fetch and replay local commits on top of the updated upstream. |
| `git push -u origin main`           | Publish `main` and set its upstream tracking branch.           |
| `git push`                          | Push to the configured upstream when one is set.               |
| `git push origin --delete <branch>` | Delete a remote branch, if permitted.                          |
| `git ls-remote origin`              | List references advertised by the remote without cloning it.   |

Example:

```
git remote add origin <YOUR-REPOSITORY-URL>
git remote -v
git push -u origin main
```

Replace the placeholder with your actual Azure Repos or GitHub URL.

Important: `origin` is only a conventional remote name. Adding it does not create an online repository. Create the repository on the hosting service first, and check its contents before your first push.

## 8. Undo, restore, and recover changes

This is one of the most important sections. Understand exactly what each command changes before using it.

| Command                       | Why / when to use it                                                                   |
| ----------------------------- | -------------------------------------------------------------------------------------- |
| `git restore <file>`          | Discard unstaged changes in a file. Destructive to those edits.                        |
| `git restore --staged <file>` | Unstage a file while keeping its working copy.                                         |
| `git reset --soft HEAD~1`     | Move the current branch back one commit, keeping changes staged.                       |
| `git reset --mixed HEAD~1`    | Move the current branch back one commit, keeping changes unstaged.                     |
| `git reset --hard HEAD~1`     | Move the branch back one commit and reset tracked files; can destroy local work.       |
| `git revert <commit-id>`      | Create a new commit that reverses an earlier commit. Usually safer for shared history. |
| `git reflog`                  | Inspect recent movements of local branch references and `HEAD`.                        |
| `git clean -n`                | Preview untracked files and directories that `git clean` would remove.                 |
| `git clean -fd`               | Delete untracked files and directories. Destructive.                                   |
| `git reset <file>`            | Unstage a file using the older reset syntax.                                           |

### Example: undo staging without losing your edits

```
git restore --staged hello.txt
```

### Example: undo a commit that has already been shared

```
git log --oneline
git revert <commit-id>
```

Use the actual commit ID. Review the changes and any conflicts before completing the revert.

### Example: inspect recovery options

```
git reflog
```

If you find a commit you need to recover, create a recovery branch before doing anything destructive:

```
git branch recovery-branch <commit-id>
```

Rule of thumb: Prefer `git revert` for undoing shared commits. Use `reset` when you deliberately want to move local history, and never use `--hard` or `clean -fd` without checking what will be lost.

## 9. Stash: temporarily put work aside

Use stash when you have unfinished changes but need to switch branches.

| Command                          | Why / when to use it                                            |
| -------------------------------- | --------------------------------------------------------------- |
| `git stash push -m "message"`    | Save tracked working-tree and staged changes in a stash.        |
| `git stash push -u -m "message"` | Include untracked files as well.                                |
| `git stash list`                 | List saved stashes.                                             |
| `git stash show -p`              | Inspect the latest stash's patch.                               |
| `git stash apply`                | Reapply the latest stash but keep it saved.                     |
| `git stash pop`                  | Reapply the latest stash and remove it if successfully applied. |
| `git stash drop`                 | Delete the latest stash entry.                                  |
| `git stash clear`                | Delete all stash entries. Destructive.                          |

Example:

```
git stash push -u -m "Customer module in progress"
git switch main
# Complete your urgent task
git switch feature/customer-module
git stash pop
```

Check `git status` after applying a stash. Conflicts can occur, and untracked files are not included unless you use `-u`.

## 10. Resolve merge conflicts

| Command                | Why / when to use it                                                       |
| ---------------------- | -------------------------------------------------------------------------- |
| `git status`           | Identify conflicted files.                                                 |
| `git diff`             | Inspect unresolved changes.                                                |
| `git diff --ours`      | Inspect the current branch's version in a conflict.                        |
| `git diff --theirs`    | Inspect the incoming version in a conflict.                                |
| `git add <file>`       | Mark a resolved file as resolved.                                          |
| `git merge --continue` | Continue a merge after resolving conflicts, when required by the workflow. |
| `git merge --abort`    | Attempt to cancel a merge in progress.                                     |

Typical workflow:

```
git status
# Open and edit each conflicted file
git add <resolved-file>
git status
git merge --continue
```

Remove conflict markers such as `<<<<<<<`, `=======`, and `>>>>>>>` from the final file. Verify the result before staging.

When to use: Whenever Git cannot automatically combine competing changes from two branches.

## 11. Advanced history: rebase and cherry-pick

| Command                       | Why / when to use it                                               |
| ----------------------------- | ------------------------------------------------------------------ |
| `git rebase main`             | Replay your current branch's commits on top of `main`.             |
| `git rebase -i HEAD~3`        | Interactively edit the last three commits in your current history. |
| `git rebase --continue`       | Continue after resolving a rebase conflict.                        |
| `git rebase --abort`          | Cancel an in-progress rebase when possible.                        |
| `git cherry-pick <commit-id>` | Apply a specific commit to the current branch.                     |
| `git cherry-pick --continue`  | Continue a cherry-pick after resolving conflicts.                  |
| `git cherry-pick --abort`     | Cancel an in-progress cherry-pick.                                 |

### Rebase example

```
git switch feature/customer-module
git fetch origin
git rebase origin/main
```

This updates your feature branch on top of the fetched remote `main`, assuming the branch and remote exist.

### Cherry-pick example

```
git switch release/1.0
git cherry-pick <commit-id>
```

Use cherry-pick when a specific fix is needed on a release branch without merging the entire feature branch.

Safety rule: Avoid rewriting commits that teammates already use unless your team has agreed to it. Rebase and cherry-pick can also create conflicts that require manual resolution.

## 12. Tags and release versions

Tags identify particular points in repository history, commonly used for software releases.

| Command                                | Why / when to use it                                       |
| -------------------------------------- | ---------------------------------------------------------- |
| `git tag`                              | List local tags.                                           |
| `git tag -l "v1.*"`                    | List tags matching a pattern.                              |
| `git tag -a v1.0.0 -m "Release 1.0.0"` | Create an annotated release tag.                           |
| `git show v1.0.0`                      | Inspect a tag and its associated commit.                   |
| `git push origin v1.0.0`               | Publish one tag.                                           |
| `git push origin --tags`               | Push all local tags that are not already present remotely. |
| `git tag -d v1.0.0`                    | Delete a local tag.                                        |
| `git push origin --delete v1.0.0`      | Delete a remote tag, subject to permissions.               |

Example:

```
git tag -a v1.0.0 -m "First stable release"
git show v1.0.0
git push origin v1.0.0
```

Only create release tags when the version is ready and consistent with your team's release process.

## 13. Inspect code and investigate bugs

| Command                                            | Why / when to use it                                     |
| -------------------------------------------------- | -------------------------------------------------------- |
| `git show HEAD`                                    | Inspect the current commit.                              |
| `git diff main..feature/customer-module`           | Compare changes between branch tips.                     |
| `git diff --check`                                 | Find whitespace errors in changes.                       |
| `git blame <file>`                                 | Inspect the commit and author associated with each line. |
| `git grep "searchText"`                            | Search tracked files for a text pattern.                 |
| `git bisect start`                                 | Begin a binary search for a problematic commit.          |
| `git bisect bad`                                   | Mark the current revision as having the problem.         |
| `git bisect good <commit-id>`                      | Mark a known-good revision.                              |
| `git bisect reset`                                 | Finish bisecting and return to the original revision.    |
| `git worktree list`                                | List working trees attached to the repository.           |
| `git worktree add ../git-experiment -b experiment` | Create a separate working directory and branch.          |

### Find which commit introduced a bug

```
git bisect start
git bisect bad
git bisect good <known-good-commit-id>
```

Git checks out revisions for you to test. Mark each tested revision with `git bisect good` or `git bisect bad` until it identifies the likely offending commit. Then finish:

```
git bisect reset
```

Use this when a regression appeared somewhere across many commits and you can reliably test whether each revision is good or bad.

## 14. `.gitignore` and repository hygiene

Use `.gitignore` to prevent unwanted files from being tracked.

Example `.gitignore` for a Node.js application:

```
node_modules/
dist/
coverage/
.env
*.log
```

| Command                       | Why / when to use it                                          |
| ----------------------------- | ------------------------------------------------------------- |
| `git check-ignore -v .env`    | Identify the ignore rule affecting `.env`.                    |
| `git ls-files`                | Check which files are already tracked.                        |
| `git rm --cached <file>`      | Stop tracking a file while leaving the working copy in place. |
| `git rm -r --cached <folder>` | Stop tracking a directory while retaining local files.        |

If `.env` was already tracked, adding it to `.gitignore` does not untrack it. For example:

```
git rm --cached .env
git add .gitignore
git commit -m "Stop tracking environment file"
```

This removes the file from future tracked snapshots, not from earlier history. If it contained a real secret, rotate the secret immediately.

## 15. Authentication and remote troubleshooting

| Command                            | Why / when to use it                                             |
| ---------------------------------- | ---------------------------------------------------------------- |
| `git remote -v`                    | Verify the remote URL.                                           |
| `git branch -vv`                   | Check upstream branch configuration.                             |
| `git fetch origin`                 | Refresh remote-tracking information.                             |
| `git ls-remote origin`             | Check whether the remote can be queried and list its references. |
| `git config --show-origin --list`  | Diagnose configuration issues.                                   |
| `git credential-manager --version` | Check Git Credential Manager availability, if installed.         |

Common errors:

- `fatal: not a git repository` — navigate to the correct repository folder.
- `remote origin already exists` — inspect `git remote -v`; use `git remote set-url origin <URL>` if you need to change it.
- `src refspec main does not match any` — check `git branch` and `git log`; the branch may not exist or may not have a commit.
- `rejected (fetch first)` — the remote may have commits missing locally. Fetch and inspect the histories before integrating them.
- `Authentication failed` — check your sign-in, credential manager, permissions, and the hosting service's supported authentication method.
- `Permission denied` — verify repository permissions and your authentication identity.

Do not paste personal access tokens, passwords, private keys, or secret URLs into chat.

## 16. Professional Git workflow for Azure DevOps

For your Terraform and Azure infrastructure repositories, use this workflow as a starting point. Follow the client's branch policies and release procedures wherever they differ.

1\. Start with the latest repository information

```
git status
git fetch origin
git branch -vv
```

Check local changes and inspect remote updates before starting work.

2\. Create a feature branch

```
git switch -c feature/terraform-validation
```

Keep your changes separate from the shared development and production branches.

3\. Validate and commit

```
git diff
git diff --check
git status
git add <specific-file>
git commit -m "Validate Terraform configuration"
```

Review the changes before staging and committing them.

4\. Push your branch

```
git push -u origin feature/terraform-validation
```

Publish the feature branch to Azure Repos.

5\. Open a pull request

Review code, pass required checks, obtain approvals, and follow the authorized deployment process.

For Terraform specifically, Git commands do not validate infrastructure by themselves. Run the appropriate Terraform formatting and validation commands, inspect the plan, and obtain the required approvals before any infrastructure changes.

## 17. The 25 commands to memorize first

git --version

Check installation

&#x20;Copy

git config --global user.name "Your Name"

Set commit author name

&#x20;Copy

git init -b main

Create a repository

&#x20;Copy

git clone \<URL>

Copy a remote repository

&#x20;Copy

git status

Check current changes

&#x20;Copy

git add \<file>

Stage a file

&#x20;Copy

git add .

Stage changes under the current directory

&#x20;Copy

git diff

Review unstaged changes

&#x20;Copy

git diff --cached

Review staged changes

&#x20;Copy

git commit -m "message"

Record a commit

&#x20;Copy

git log --oneline

View commit history

&#x20;Copy

git branch

List local branches

&#x20;Copy

git switch -c \<branch>

Create and switch branches

&#x20;Copy

git switch main

Switch to main

&#x20;Copy

git merge \<branch>

Merge another branch

&#x20;Copy

git remote -v

Inspect remotes

&#x20;Copy

git fetch origin

Download remote updates

&#x20;Copy

git pull

Integrate upstream changes

&#x20;Copy

git push -u origin main

Publish main and set upstream

&#x20;Copy

git stash

Temporarily save changes

&#x20;Copy

git restore --staged \<file>

Unstage a file

&#x20;Copy

git revert \<commit-id>

Reverse a commit safely in shared history

&#x20;Copy

git tag -a v1.0.0 -m "Release"

Create a version tag

&#x20;Copy

git reflog

Inspect recent local reference movements

&#x20;Copy

git diff --check

Check whitespace errors

&#x20;Copy

## 18. Safety rules you should always remember

- Never use `git reset --hard`, `git clean -fd`, or force-push without understanding the consequences.
- Never commit passwords, tokens, `.env` files, or private keys.
- Never push directly to a protected production branch if the team requires pull requests.
- Always check `git status` before committing, switching branches, or resolving conflicts.
- Review `git diff` before staging and `git diff --cached` before committing.
- Do not assume that a successful Git push means the application has been deployed.
- Remember that `git revert` preserves shared history better than resetting a shared branch.

## Official references

- [Pro Git book — complete learning guide](https://git-scm.com/book/en/v2?utm_source=chatgpt.com)
- [Git command reference](https://git-scm.com/docs?utm_source=chatgpt.com)
- [Microsoft Learn — Azure Repos Git](https://learn.microsoft.com/en-us/azure/devops/repos/git/?utm_source=chatgpt.com)
- [GitHub — Using Git](https://docs.github.com/en/get-started/using-git?utm_source=chatgpt.com)
