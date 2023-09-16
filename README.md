# <img src=https://upload.wikimedia.org/wikipedia/commons/3/3f/Git_icon.svg width ="30">Git Command Line Tutorial  <!-- omit from toc -->

## Introduction

Mastering Git and understanding source control workflows is a fundamental skill for professionals in software engineering, data science, and virtually anyone involved in coding.

This proficiency proves invaluable when collaborating within a team, but it's equally advantageous for individual developers working on personal projects. Git is often one of those skills that are expected to be picked up along the way, rather than formally tought.

From my perspective, many developers are quite comfortable using graphical user interfaces to work with Git. These GUIs, such the [source control features in VS Code](https://code.visualstudio.com/docs/sourcecontrol/overview), enhanced with extensions (I personally enjoy using [Git Graph](https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph) and [Commit Message Editor](https://marketplace.visualstudio.com/items?itemName=adam-bender.commit-message-editor) extensions), unquestionably make Git more user-friendly. However, it's important to remember that there are still some compelling reasons to explore the power of bare-bones command line.

Git's Command Line Interface (CLI) is cross-platform, ensuring consistent performance across all your working environments. Through consistent practice, employing the command line can push developers to establish more effective Git workflows. Additionally, delving into Git CLI compels us to grasp basic terminal commands, an indispensable skill for any software developer.

This tutorial assumes you possess a baseline understanding of source control workflows and Git's fundamentals, and serves as both a valuable refresher for experienced Git users and an educational resource for those looking to deepen their Git knowledge.

We'll begin by revisiting essential Linux commands before diving into a comprehensive exploration of various Git commands. These include initializing repositories, staging and committing files, examining revision history, managing branches, merging changes, comparing alterations, and techniques for rewriting Git history. Along the way, I'll provide practical demonstrations to ensure you grasp these concepts thoroughly.

Learning Git and source control workflows is essential for software engineers, data scientists, and practically anybody writing code.

It is incredibly important for anybody working on a team, but also beneficial for individual developers working on personal projects. Git is one of those skills which are usually never tought properly, and it is assumed that you pick up along the way.

## Table of Contents

- [Introduction](#introduction)
- [Table of Contents](#table-of-contents)
- [General Commands](#general-commands)
- [Git Commands](#git-commands)
  - [Basics](#basics)
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
    - [Ammending History](#ammending-history)
    - [Editing Commit Messages](#editing-commit-messages)
    - [Example: Editting a Commit Message](#example-editting-a-commit-message)
    - [Deleting a commit](#deleting-a-commit)
    - [Reordering commits](#reordering-commits)
    - [Squashing Commits](#squashing-commits)
    - [Example: Squashing Commits](#example-squashing-commits)
    - [Splitting commits](#splitting-commits)

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

## Git Commands

### Basics

#### Initializing a repository

1. `git init`:
Initializes a new Git repository in the current directory, creating a hidden ".git" folder to manage version control.
2. `git version`:
Displays the installed Git version.
3. `git status`:
Shows the status of your Git repository, indicating which files have been modified, added, or deleted. The `-s` or `--short`` option provides a more concise output.

#### Example: Initializing a git repository

See [Example](./examples/git-init-example.md).

### Staging and Committing Changes

#### Staging / Restoring Changes

1. `git add README.md`:
Stages the "README.md" file for the next commit, adding it to the index.
2. `git add .`:
Stages all changes in the current directory for the next commit.
3. `git restore UNSTAGED_FILE.md`:
Discards unstaged changes in the file "UNSTAGED_FILE.md" and reverts it to the last committed version.
4. `git rm --cached STAGED_FILE.md`:
Unstages the changes in the file "STAGED_FILE.md" that were previously added to the index.

#### Commiting Changes

1. `git commit -m "my first commit"`:
Commits the staged changes with a descriptive commit message.

#### Logging History

1. `git log --graph --oneline --all`:
Displays the commit history of the repository. The --graph option visualizes the commit history as a graph, and other options can format the log output.

#### Example: Staging and Committing Changes

See [Example](./examples/git-commit-example.md).

### Working with Branches

#### Branching

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

#### Merging Branches

1. `git merge feat-branch`:
Merges changes from the "feat-branch" into the current branch, with an optional merge message provided using the -m flag.

#### Comparing Changes

1. `git diff`:
Shows the difference between the working directory and the last commit.
2. `git diff --cached`:
Displays the changes between the staged (index) and the last commit.
3. `git diff a85eb2f 3504f34`:
Compares two specific commits, identified by their hash values.
4. `git diff feature_branch master (on feature branch)`:
Compares the differences between "feature_branch" and "master" branches.

#### Example: Working with Branches

See [Example](./examples/git-branching-example.md).

### Rewriting History

#### Ammending History

1. `git commit --amend`
Adds changes to previous commit (or editting last commit message)
2. `git commit --amend --no-edit`
Adds changes to previous commit without editting the last commit message.

#### Editing Commit Messages

`git rebase -i --root`
Interactive rebase: shows menu for all commits since root.

To reword a specific commit, add rename `pick` to `reword` in front of the commit:

#### Example: Editting a Commit Message

See [Example](./examples/git-edit-message.md).

#### Deleting a commit

Again, use the `git rebase -i --root` to display all previous commits (as an example), reword `pick` in front of the desired commit to `drop`, save and exit (`esc + :wq`)

#### Reordering commits

From the `git rebase -i --root` menu, reorder the commits (maintain the `pick` prefix).

#### Squashing Commits

Assuming you have From the `git rebase -i --root` menu, and we want to "squash" 3rd and 2nd commits to 1st commit.

We will change `pick` to `squash` prefix on the 2nd and 3rd commits.

#### Example: Squashing Commits

See [Example](./examples/git-squash-example.md).

#### Splitting commits

1. Enter the rebase-todo menu with `git rebase -i --root`.
2. Modify the prefix for the commit you want to split from `pick` to `edit`.
3. Then `git reset HEAD^` to "unstage" files from the commit we specified to edit. We can verify this with `git status --short`.
4. Now use `git add` and `git commit` the specific changes seperately.
5. Finally `git rebase --continue` to exit the rebase progress. Verify the commit has been split with `git log --oneline`.

See [Example](./examples/git-split-commits.md).

Hope this tutorial helped you!
