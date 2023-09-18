# <img src=https://upload.wikimedia.org/wikipedia/commons/3/3f/Git_icon.svg width ="30">Git Command Line Tutorial  <!-- omit from toc -->

## Introduction

Mastering Git and understanding source control workflows is a fundamental skill for professionals in software engineering, data science, and virtually anyone involved in coding.

This proficiency proves invaluable when collaborating within a team, but it's equally advantageous for individual developers working on personal projects. Git is often one of those skills that are expected to be picked up along the way, rather than formally tought.

From my perspective, many developers are quite comfortable using graphical user interfaces to work with Git. As an example, I personally enjoy using the [source control features in VS Code](https://code.visualstudio.com/docs/sourcecontrol/overview), enhanced with the [Git Lens](https://www.gitkraken.com/gitlens) extension, which unquestionably make Git more user-friendly. However, it's important to remember that there are still some compelling reasons to explore the power of bare-bones command line.

Git's Command Line Interface (CLI) is cross-platform, ensuring consistent performance across all your working environments. Through consistent practice, employing the command line can push developers to establish more effective Git workflows. Additionally, delving into Git CLI compels us to grasp basic terminal commands, an indispensable skill for any software developer.

This tutorial assumes you possess a baseline understanding of source control workflows and Git's fundamentals, and serves as both a valuable refresher for experienced Git users and an educational resource for those looking to deepen their Git knowledge.

We'll begin by revisiting essential commands before diving into a comprehensive exploration of various Git commands. These include initializing repositories, staging and committing files, examining revision history, managing branches, merging changes, comparing alterations, and techniques for rewriting Git history. Along the way, I'll provide practical demonstrations to ensure you grasp these concepts thoroughly.

## Table of Contents

- [Introduction](#introduction)
- [Table of Contents](#table-of-contents)
- [General Commands](#general-commands)
- [Git Basics](#git-basics)
  - [Initializing a repository](#initializing-a-repository)
  - [Example: Initializing a git repository](#example-initializing-a-git-repository)
- [Staging and Committing Changes](#staging-and-committing-changes)
  - [Staging / Restoring Changes](#staging--restoring-changes)
  - [Commiting Changes](#commiting-changes)
  - [Logging History](#logging-history)
  - [Example: Staging and Committing Changes](#example-staging-and-committing-changes)
- [Working with Branches](#working-with-branches)
  - [Branching](#branching)
  - [Merging Branches](#merging-branches)
  - [Comparing Changes](#comparing-changes)
  - [Example: Working with Branches](#example-working-with-branches)
- [Rewriting History](#rewriting-history)
  - [Resetting Commits](#resetting-commits)
  - [Reverting Commits](#reverting-commits)
  - [Ammending History](#ammending-history)
  - [Editing Commit Messages](#editing-commit-messages)
  - [Example: Editting a Commit Message](#example-editting-a-commit-message)
  - [Deleting a commit](#deleting-a-commit)
  - [Reordering commits](#reordering-commits)
  - [Squashing Commits](#squashing-commits)
  - [Example: Squashing Commits](#example-squashing-commits)
  - [Splitting commits](#splitting-commits)
- [Working with Remote Git Servers](#working-with-remote-git-servers)
  - [Initial Configuration](#initial-configuration)
  - [Cloning Repositories](#cloning-repositories)
  - [Forking Repositories](#forking-repositories)
  - [Fetching, Pulling and Pushing](#fetching-pulling-and-pushing)
  - [Remote Merges (Pull Requests)](#remote-merges-pull-requests)

## General Commands

For the sake of completeness, I'll review the most basic linux commands which we will use together with git.

1. `pwd`:
Print Working Directory - Displays the current directory or folder path in the command line.
2. `ls`:
List - Lists the files and directories in the current directory.
3. `ls -a`:
List All - Lists all files and directories in the current directory, including hidden ones.
4. `cd ~`: Change current working directory to the home directory
5. `cd \`:
Change the current working directory to the root directory.
6. `touch README.md`:
Creates an empty file named "README.md" in the current directory.
7. `echo some text >> README.md`:
Appends the text "some text" to the "README.md" file.
8. `nano README.md`:
Opens the "README.md" file in the [nano](https://www.nano-editor.org/) text editor for editing.
9. `cat README.md`:
Displays the contents of the "README.md" file in the terminal.
10. `rm README.md`:
Removes or deletes the "README.md" file.
11. `rmdir directory`:
Removes or deletes an empty directory named "directory."
12. `ls | tee /path/to/output.txt`:
Executes the command `ls` and saves both its standard output and error output to a file at the specified path.
13. `tree .`: displays tree structure of current working directory (needs to be installed - see this [tutorial](https://www.geeksforgeeks.org/tree-command-unixlinux/).

## Git Basics

### Initializing a repository

1. `git init`:
Initializes a new Git repository in the current directory, creating a hidden ".git" folder to manage version control.
2. `git version`:
Displays the installed Git version.
3. `git status`:
Shows the status of your Git repository, indicating which files have been modified, added, or deleted. The `-s` or `--short`` option provides a more concise output.
4. `git config --global user.name John Snow`
Sets the global Git user name. This will be the default signature on commits.
5. `git config --global user.email john.snow@gmail.com`
Sets the global Git user email address. This will be the default signature on commits.

### Example: Initializing a git repository

See [Example](./examples/git-init-example.md).

## Staging and Committing Changes

### Staging / Restoring Changes

1. `git add README.md`:
Stages the "README.md" file for the next commit, adding it to the index.
2. `git add .`:
Stages all changes in the current directory for the next commit.
3. `git restore UNSTAGED_FILE.md`:
Discards unstaged changes in the file "UNSTAGED_FILE.md" and reverts it to the last committed version.
4. `git rm --cached STAGED_FILE.md`:
Unstages the changes in the file "STAGED_FILE.md" that were previously added to the index.

### Commiting Changes

1. `git commit -m "my first commit"`:
Commits the staged changes with a descriptive commit message.

### Logging History

1. `git log --graph --oneline --all`:
Displays the commit history of the repository. The --graph option visualizes the commit history as a graph, and other options can format the log output.

### Example: Staging and Committing Changes

See [Example](./examples/git-commit-example.md).

## Working with Branches

### Branching

1. `git branch`:
Lists all the branches in the Git repository.
2. `git branch new-branch-name`:
Creates a new branch named "new-branch-name."
3. `git branch -d old-branch (git branch --delete old-branch)`:
Deletes the specified branch "old-branch."
4. `git switch feat-branch`:
Switches to the branch "feat-branch."
5. `git switch –create feat-branch` / `git switch -c feat-branch`:
Creates and switches to a new branch named "feat-branch."
6. `git branch -m original_branch_name new_branch_name` / `git branch --move original_branch_name new_branch_name`:
Renames a branch from "original_branch_name" to "new_branch_name."

### Merging Branches

1. `git merge feat-branch`:
Merges changes from the "feat-branch" into the current branch, with an optional merge message provided using the -m flag.

### Comparing Changes

1. `git diff`:
Shows the difference between the working directory and the last commit.
2. `git diff --cached`:
Displays the changes between the staged (index) and the last commit.
3. `git diff a85eb2f 3504f34`:
Compares two specific commits, identified by their hash values.
4. `git diff feature_branch master (on feature branch)`:
Compares the differences between "feature_branch" and "master" branches.

### Example: Working with Branches

See [Example](./examples/git-branching-example.md).

## Rewriting History

### Resetting Commits

Git's `HEAD` keyword always marks your location. We can use `HEAD` to reference previous commits with the `~` operator (or `^` operator when merging commits). For example `HEAD~3` references three commits back from current location, `HEAD~1` (shortformed as `HEAD~`) will reference one commit back.

Git's `reset` command moves `HEAD` and branch to the specified commit. The additional options (`--soft`, `--mixed`, `--hard`) will specify what we want to do 

1. `git reset 1dded2a`
Will move `HEAD` to the specified commit ID. Changes from `HEAD` will move to the working directory.
2. `git reset HEAD~`
Will move `HEAD` one commit back.
3. `git reset HEAD~2`
Will move `HEAD` two commits back.
4. `git reset --soft HEAD~`
Undoes the commit `HEAD` points to, and moves those changes from the object database to the *index* (staging area).
5. `git reset --mixed HEAD~` / `git reset HEAD~`
Undoes the commit `HEAD` points to, and moves those changes from the object database to the *working directory*
6. `git reset --hard`
Undoes the commit `HEAD` points to, and *deletes* changes on `HEAD` (**be careful with this - the hard mode is destructive and changes on `HEAD` cannot be restored**)

### Reverting Commits

Reverting commits is similar to *resetting* commits, but differs in that it creates an "anti-commit"

1. `git revert HEAD`
This will undo the changes done on the current commit, and create a new "anti commit".
2 `git revert HEAD~`
Will create an "anti-commit", reverting both the current and previous commits.

### Ammending History

1. `git commit --amend`
Adds changes to previous commit (or editting last commit message)
2. `git commit --amend --no-edit`
Adds changes to previous commit without editting the last commit message.

### Editing Commit Messages

`git rebase -i --root`
Interactive rebase: shows menu for all commits since root.

To reword a specific commit, add rename `pick` to `reword` in front of the commit:

### Example: Editting a Commit Message

See [Example](./examples/git-edit-message.md).

### Deleting a commit

Again, use the `git rebase -i --root` to display all previous commits (as an example), reword `pick` in front of the desired commit to `drop`, save and exit (`esc + :wq`)

### Reordering commits

From the `git rebase -i --root` menu, reorder the commits (maintain the `pick` prefix).

### Squashing Commits

Assuming you have From the `git rebase -i --root` menu, and we want to "squash" 3rd and 2nd commits to 1st commit.

We will change `pick` to `squash` prefix on the 2nd and 3rd commits.

### Example: Squashing Commits

See [Example](./examples/git-squash-example.md).

### Splitting commits

1. Enter the rebase-todo menu with `git rebase -i --root`.
2. Modify the prefix for the commit you want to split from `pick` to `edit`.
3. Then `git reset HEAD^` to "unstage" files from the commit we specified to edit. We can verify this with `git status --short`.
4. Now use `git add` and `git commit` the specific changes seperately.
5. Finally `git rebase --continue` to exit the rebase progress. Verify the commit has been split with `git log --oneline`.

See [Example](./examples/git-split-commits.md).

## Working with Remote Git Servers

### Initial Configuration

1. `git remote add <name> <url>`
Will add a repository on a remote server as the remote repo for our local repo. Usually, name is set to `origin`.
2. `git remote rm <name>`
Remove an the connection to a remote repository.
3. `git remote -v`
Will list the remote repository or repositories URL(s).
4. `git config push.default simple`
Pushes the current branch to its upstream branch, as long as the local and upstream branch names match.
5. `git config pull.rebase`
Print the stategy for pulling. This can be set to true or false (false by default).

### Cloning Repositories

1. `git clone https://github.com/user-name/repo-name.git`
Creates a local copy of a repository stored on a remote server (e.g. GitHub, Gitlab, Bitbucket, etc.). On GitHub, the simplest way to clone is via `HTTPS` which requries no additional setup. However, we can clone via `SSH`. The `clone` command creates a local `.git` folder inside the cloned repository, which includes all commits, branches, and metadata. After cloning you should use `git switch` to switch to a desired branch name (the default is the `main` or `master` branch).

2. `git clone https://github.com/user-name/repo-name.git local-repo-name`
changes the default name of the folder from the repository name to a custom name ()`local-repo-name` here).

### Forking Repositories

*Forking* is a GitHub feature, which allows us to create your own copy (under your own username) of any public repository on GitHub, and make changes to it.

This allows you to work on open-source projects without the need to add grant addititional permissions to individual collaborators in the respository settings on GitHub.

Usually, if we want to make changes to an open-source project, it is best we first *fork* the repository to our own account (via the GitHub UI) and only then clone it locally. Read more about forking on GitHub [here](https://docs.github.com/en/get-started/quickstart/fork-a-repo).

### Fetching, Pulling and Pushing

1. `git remote -v`
List the remote repository connection(s). Useful for knowing where to fetch, pull and push from. The default name is `origin`.
2. `git fetch`
Fetch updates your local repository with changes from the remote repository. It *fetches* changes but does not force you to actually merge the changes into your repo. This is the same as `git fetch origin`.
3. `git fetch <remote>`
In case there are multiple remote connections to a repository, you can fetch from a specific one.
4. `git fetch <remote> <branch>`
Allows you to fetch a specific branch from a specific remote repository.
5. `git push`
Pushes local commits to the remote repository. In many cases, you will be prompted for a username and password to the remote repository. Some remote git servers use personal access tokens instead. You can store this password on your machine's credential manager (e.g. Keychain Access on Mac or Credentials Manager on Windows) so that you won't be prompted every time. This is the same as `git push origin`.
6. `git push --set-upstream <remote> <local-branch>` or `git push -u <remote> <local-branch`
The standard `git push` command will only work if the current branch has an `upstream` (or `tracking`) branch. When creating a new local branch, you will need to configure its remote `upstream branch`. This only has to be done once for a new branch. The default `<remote>` repository connection is named `origin`.
7. `git pull`
This command is a `git fetch` + `git merge` command. It fetches the upstream branches from the remote repository, and then merges the changes of the upstream branch you are on locally.

### Remote Merges (Pull Requests)

Once pushing a local branch to a remote repository, we can merge it on the remote server with another branch (usually this is a `development` branch). The remote merge is called a *Pull Request*, and is done via the remote server web interface. Once the pull request is approved the default reviewers (set on the remote server), the branch can then be merged. Note that while `pull` and `pull request` sound similar, they mean completely different things. Read more about creating pull requests on GitHub [here](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request).

Hope this tutorial helped you!
