# <img src=https://upload.wikimedia.org/wikipedia/commons/3/3f/Git_icon.svg width ="30">Git Command Line Tutorial

## Introduction

Learning Git and source control workflows is essential for software engineers, data scientists, and practically anybody writing code.

It is incredibly important for anybody working on a team, but also beneficial for individual developers working on personal projects. Git is one of those skills which are usually never tought properly, and it is assumed that you pick up along the way.

While there are many graphical user interfaces today which assist with git source control as development tools (my favorites include [source control in VS Code](https://code.visualstudio.com/docs/sourcecontrol/overview), with the [Git Graph](https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph) and [Commit Message Editor](https://marketplace.visualstudio.com/items?itemName=adam-bender.commit-message-editor) extensions), I'd argue there are still some benefits to using the bare-bone command line!

There are several arguments to this:

- Git CLI (command line interface) is cross-platform, meaning it will work the same on any machine you work on.
- With some practice, I'd argue using command line will force us developers to get a better git workflow.
- Finally, as a side effect, I believe learning git CLI forces us to learn basic commands and get comfortable with the terminal. Which is essential to any software developer.

This tutorial assumes you have some knowledge of the source control workflow and how git works, and can be a good refresher for anybody working with git in some form.

I'll start with reviewing general linux commands, and then move on to more various git commands for initializing a repository, staging and commiting files, logging history, branching, merging, comparing changes, logging and rewriting history. I will also present some short demos of how they work.

## Table of Contents

- [Git Command Line Tutorial](#git-command-line-tutorial)
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
      - [Example: Merging Branches](#example-merging-branches)
      - [Example: Merging Conflicting Branches](#example-merging-conflicting-branches)
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

(back to [Table of Contents](#table-of-contents))

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

Let's show the workflow for creating a new git repository in the home directory `~` inside a directory named `git-demo`:

```shell
cd ~
mkdir git-demo
cd git-demo
```

Ensuring Git is properly installed on our machine (otherwise install from [here](https://git-scm.com/)):

```shell
git version
```

Now Initializing the repository:

```shell
git init
ls -a
```

will output:

```text
Initialized empty Git repository in /Users/username/git-demo/.git/
.       ..      .git
```

We can see that we created a hidden folder `.git` which will manage the source control for us. We can examine the contents of this folder with the `tree` command:

```shell
tree .git
```

which will output the following:

```text
.git
├── HEAD
├── config
├── description
├── hooks
│   ├── applypatch-msg.sample
│   ├── commit-msg.sample
│   ├── fsmonitor-watchman.sample
│   ├── post-update.sample
│   ├── pre-applypatch.sample
│   ├── pre-commit.sample
│   ├── pre-merge-commit.sample
│   ├── pre-push.sample
│   ├── pre-rebase.sample
│   ├── pre-receive.sample
│   ├── prepare-commit-msg.sample
│   ├── push-to-checkout.sample
│   └── update.sample
├── info
│   └── exclude
├── objects
│   ├── info
│   └── pack
└── refs
    ├── heads
    └── tags
```

It is not necessary to understand the internals of the `.git` folder but good to be familiar with it, since this is where all changes will be tracked.

Finally, we can use `git status` which will output the following:

```text
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

We can see that Git is initialized, and we are on a branch called main.

(back to [Table of Contents](#table-of-contents))

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

(back to [Table of Contents](#table-of-contents))

#### Example: Staging and Committing Changes

```shell
cd ~
mkdir git-demo
cd git-demo

git init
```

Lets create a README.md file and add some text to it:

```shell
touch README.md
echo This is the README file for my project >> README.md
```

Let's verify that we created the file with `ls -a`:

```text
.git
README.md
```

We can check that our text was added to the README file using the `cat README.md` command which will output:

```text
This is the README file for my project
```

Great! Now let's verify the status of the git repository:

```shell
git status --short
```

will output:

```text
?? README.md
```

the `??` prefix indicates that the file is not tracked by git, and not staged.

Let's stage this file:

```shell
git stage README.md
```

and now `git status --short` will output:

```shell
A  README.md
```

The prefix `A` means that the file is added to git's index.

If we modify this file, for example adding a period at the end of the sentence:

```text
This is the README file for my project.
```

We can edit this file in the terminal using [nano](https://www.nano-editor.org/) with the `nano README.md` command. After editting the file, we can save and exit with `^X`.

then `git status --short` will output:

```shell
AM README.md
```

The `AM` prefix means the file was previously added to git's staging area, but has been modified since.

We can revert our unstaged modification with:

```shell
git restore README.md
```

now, the period at the end of the sentence is removed and `git status --short` will remove change the file's status from `AM` back to `A`.

Let's commit this file:

```shell
git commit -m "adding a README.md file"
```

To see our changes, we can use:

```shell
git log --oneline
```

which will output the commits in a single line per commit as follows:

```text
7f6ba87 (HEAD -> main) added a README.md file
```

Now, `git status` will display

```text
On branch main
nothing to commit, working tree clean
```

Great! Let's add two more commits for practice:

```shell
echo adding some text for the second commit >> README.md
git add README.md
git commit -m "adding text to README.md"

echo adding even more text for the third commit >> README.md
git add README.md
git commit -m "adding even more text to README.md"
```

Let's verify our modifications

```shell
cat README.md
```

will output:

```text
This is the README file for my project
adding some text for the second commit
adding even more text for the third commit
```

Let's print the history of our main branch:

```shell
git log --oneline
```

will output:

```text
3cd8dc2 (HEAD -> main) adding even more text to README.md
bf708cc adding text to README.md
7f6ba87 added a README.md file
```

Great! At this stage, `git status` will notify us that there are no changes as expected.

(back to [Table of Contents](#table-of-contents))

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

(back to [Table of Contents](#table-of-contents))

#### Example: Working with Branches

Let's set up a clean repository, and make some commits.

```shell
cd ~
mkdir git-demo

git init

touch README.md

echo This is the README file for my project >> README.md
git add README.md
git commit -m "added a README.md file"

echo adding some text for the second commit >> README.md
git add README.md
git commit -m "adding text to README.md"

echo adding even more text for the third commit >> README.md
git add README.md
git commit -m "adding even more text to README.md"
```

Now `git log --oneline` will display:

```text
3cd8dc2 (HEAD -> main) adding even more text to README.md
bf708cc adding text to README.md
7f6ba87 added a README.md file
```

Git log tells us that we are on the main branch and have 3 commits.

Let's create a new feature branch called `feat-branch`:

```shell
git branch feat-branch
```

Let's verify the existing branches:

```shell
git branch
```

which will output

```text
  feat-branch
* main
```

We can see the two branches, and the asterix `*` prefix specifies that we are on the `main` branch.

To switch to the `feat-branch` branch, we willuse the `switch command`:

```shell
git switch feat-branch
```

This will output `Switched to branch 'feat-branch'` and we can verify this with `git branch` which will output:

```text
* feat-branch
  main
```

Note that the asterix as moved to the `feat-branch` as expected!

Now let's edit our `README.md` file, and commit our change

```shell
echo adding some text describing the feature branch >> README.md

git add README.md
git commit -m "modifications for feature branch"
```

Let's examine what happened with `git log --oneline`:

```text
4780c3b (HEAD -> feat-branch) modifications for feature branch
3cd8dc2 (main) adding even more text to README.md
bf708cc adding text to README.md
7f6ba87 added a README.md file
```

We can see that the `HEAD` points to `feat-branch` while the `main` branch is one commit behind!

(back to [Table of Contents](#table-of-contents))

#### Example: Merging Branches

Continuing the previous example, let's merge our change with the `main` branch. To do this, we will switch back to the `main` branch, and then merge.

```shell
git switch main
git merge feat-branch
git log --oneline
```

This will output:

```text
4780c3b (HEAD -> main, feat-branch) modifications for feature branch
3cd8dc2 adding even more text to README.md
bf708cc adding text to README.md
7f6ba87 added a README.md file
```

We can see that `HEAD` now points to both `main` and `feat-branch`, and both branches have the same commit hash!

Now that we are done with our "feature", we can delete our `feat-branch`:

```shell
git branch --delete feat-branch
```

This will output `Deleted branch feat-branch (was 4780c3b).`

(back to [Table of Contents](#table-of-contents))

#### Example: Merging Conflicting Branches

Now, let's showcase merge conflicts. We'll create another branch `feat-b` but now edit the existing text in the `README.md` file.

```shell
git switch --create feat-b
```

Now we created, and switched to `feat-b` in a single command.

Let's edit the text in `README.md`. As an example, we'll change the word "project" to "demo". Now the text will be as follows:

```text
This is the README file for my demo
adding some text for the second commit
adding even more text for the third commit
adding some text describing the feature branch
```

Before committing, let's compare our change with Git's tracked version from before the change.

```shell
git diff README.md
```

This will output the following:

```text
diff --git a/README.md b/README.md
index 37f1de3..07d8fdd 100644
--- a/README.md
+++ b/README.md
@@ -1,4 +1,4 @@
-This is the README file for my project
+This is the README file for my demo
 adding some text for the second commit
 adding even more text for the third commit
 adding some text describing the feature branch
```

Here, the important lines are:

```text
-This is the README file for my project
+This is the README file for my demo
```

The `-` prefix specifies the original row in the file, while the `+` prefix specifies the new version of the file.

Let's stage and commit this change on our `feat-b` branch.

```shell
git add README.md
git commit -m "reworded 'project' to 'demo' in README.md"
```

Now `git log --oneline` outputs:

```text
0b218d4 (HEAD -> feat-b) reworded 'project' to 'demo' in README.md
4780c3b (main) modifications for feature branch
3cd8dc2 adding even more text to README.md
bf708cc adding text to README.md
7f6ba87 added a README.md file
```

Now, let's switch to main, and change "project" to "repo"

```shell
git switch main
```

```text
This is the README file for my repo
adding some text for the second commit
adding even more text for the third commit
adding some text describing the feature branch
```

Let's commit our change on `main` and try to merge `feat-b`:

```shell
git add README.md
git commit -m "changed 'project' to 'repo'"
```

If we log Git's history now (using some additional options):

```shell
git log --oneline --graph
```

We get:

```text
* 5a64154 (HEAD -> main) changed 'project' to 'repo'
| * 957cf1b (feat-b) reworded 'project' to 'demo' in README.md
|/  
* 4780c3b modifications for feature branch
* 3cd8dc2 adding even more text to README.md
* bf708cc adding text to README.md
* 7f6ba87 added a README.md file
```

We can see that `main` has "seperated" from the `feat-b` stem. This means that a change was first committed on `feat-b` and only then a change was committed on `main`.

Let's try to merge `feat-b` to main and see what happens!

```shell
git merge feat-b
```

will output:

```text
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
```

Git is notifying us of a conflict, since in `feat-b` the word `project` was changed to `demo` while on `main` it was changed to `repo`.

Inspecting `git status --short` will output:

```text
UU README.md
```

The prefix `UU` notifies us that the files are unmerged!

Lets see the contents of `README.md`

```shell
cat README.md
```

will output:

```text
<<<<<<< HEAD
This is the README file for my repo
=======
This is the README file for my demo
>>>>>>> feat-b
adding some text for the second commit
adding even more text for the third commit
adding some text describing the feature branch
```

Let's explain whats going on here! Git added markers to our conflicted file. The `<<<<<<< HEAD` prefix shows the modification in our `main` branch (`repo`), the `=======` seperates this modification from the modification on the `feat-b` branch which ends with the `>>>>>>> feat-b` suffix.

To solve the merge, we need to *manually* edit the file, remove the conflict markers, and keep the modification which we want for our merge.
In our case, let's assume we want `demo` and not `repo`.

After modifying our file, it looks like this:

```text
This is the README file for my demo
adding some text for the second commit
adding even more text for the third commit
adding some text describing the feature branch
```

Now, to complete the merge, we'll add and commit our change:

```shell
git add README.md
git commit -m "Solved merge conflict, kept 'demo' from feat-b instead of 'repo' from 'main'"
```

Finally, let's view our git graph by running

```shell
git graph --oneline --graph --all
```

```shell
*   e8f73b1 (HEAD -> main) Solved merge conflict, kept 'demo' from feat-b instead of 'repo' from 'main'
|\  
| * 957cf1b (feat-b) reworded 'project' to 'demo' in README.md
* | 5a64154 changed 'project' to 'repo'
|/  
* 4780c3b modifications for feature branch
* 3cd8dc2 adding even more text to README.md
* bf708cc adding text to README.md
* 7f6ba87 added a README.md file
```

We can see that `feat-b` was merged to main and our message states that the conflict was solved.

(back to [Table of Contents](#table-of-contents))

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

Let's initialize our repository in the home `~` directory, and create three files `a`, `b` and `c` make some commits:

```shell
cd ~
mkdir git-demo

git init

touch a
git add a
git commit -m "frist commit"

touch b
git add b
git commit -m "second commit"

touch c
git add c
git commit -m "third commit"
```

If we run `git log --oneline`, we notice that we made a typo on the first commit `frist` instead of `first`... oops!

Let's fix this.= by running

```shell
git rebase -i --root
```

The first lines will show:

```text
pick 766f449 my frist commit
pick 6106de8 my second commit
pick 94bfe32 my third commit
```

Note the typo on the first commit. To edit the commit message, change `pick` to `reword` without editting the message (enter vim with `i`):

```text
reword 766f449 my frist commit
pick 6106de8 my second commit
pick 94bfe32 my third commit
```

Then quit the text editor and save changes with `esc + :wq` in vim.

A `.git/COMMIT_EDITMSG` file will open in vim, which will display the commit message:

```text
my frist commit
```

Modify the text (`i` to enter):

```text
my first commit
```

exit and save (`esc + :wq`).

Verify the edited commit message with `git log --oneline`.

(back to [Table of Contents](#table-of-contents))

#### Deleting a commit

Again, use the `git rebase -i --root` to display all previous commits (as an example), reword `pick` in front of the desired commit to `drop`, save and exit (`esc + :wq`)

#### Reordering commits

From the `git rebase -i --root` menu, reorder the commits (maintain the `pick` prefix).

#### Squashing Commits

Assuming you have From the `git rebase -i --root` menu, and we want to "squash" 3rd and 2nd commits to 1st commit.

We will change `pick` to `squash` prefix on the 2nd and 3rd commits.

#### Example: Squashing Commits

Continuing from our previous example:

```text
pick 766f449 my first commit
pick 6106de8 my second commit
pick 94bfe32 my third commit
```

will change to:

```text
pick 766f449 my first commit
squash 6106de8 my second commit
squash 94bfe32 my third commit
```

after saving and exiting (`esc + :wq`), the `.git/COMMIT_EDITMSG` file will open in vim.

showing the following:

```text
# This is a combination of 3 commits.
# This is the 1st commit message:

first commit

# This is the commit message #2:

second commit

# This is the commit message #3:

third commit

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date:      Wed Sep 13 23:47:19 2023 +0300
#
# interactive rebase in progress; onto 1bc2565
# Last commands done (3 commands done):
#    squash 629e5a5 second commit
#    squash 64bd681 third commit
# No commands remaining.
# You are currently rebasing branch 'main' on '1bc2565'.
#
```

Here we can edit the message for the squashed commit. Let's change it to:

```text
adding files a, b and c
```

Then save and quit (`esc + :wq`).

Finally `git log --oneline` will verify that the commits have been squashed:

```text
1dded2a (HEAD -> main) adding files a, b and c
```

`git status` will indicate that we are on a clean tree, and `ls` will show that all three files, `a` , `b` and `c` are present!

(back to [Table of Contents](#table-of-contents))

#### Splitting commits

1. Enter the rebase-todo menu with `git rebase -i --root`.
2. Modify the prefix for the commit you want to split from `pick` to `edit`.
3. Then `git reset HEAD^` to "unstage" files from the commit we specified to edit. We can verify this with `git status --short`.
4. Now use `git add` and `git commit` the specific changes seperately.
5. Finally `git rebase --continue` to exit the rebase progress. Verify the commit has been split with `git log --oneline`.

Let's show an example of this in a brand new git repo, which we will create in our home folder (`~`):

```shell
cd ~

mkdir git_demo
cd git-demo
```

Now, initialize the git repository and add 4 files in 3 commits:

```shell
git init

touch a
git add a
git commit -m "added a"

touch b c
git add b c
git commit -m "added b and c"

touch d
git add d
git commit -m "added d"
```

We can log our commits with `git log --oneline`, which will output:

```text
d099da5 (HEAD -> main) added d
99d52e1 added b and c
26fe748 added a
```

Now, let's assume we want to split b and c into two seperate commits.

We'll enter the interactive rebase todo menu:

```shell
git rebase -i --root
```

Which will display the following output in a vim text editor:

```text
pick 26fe748 added a
pick 99d52e1 added b and c
pick d099da5 added d

# Rebase d099da5 onto 60df0ae (3 commands)
```

We'll change the second commit prefix from `pick` to `edit` (in vim, `i` to insert text, exit and save with `esc + :wq`).

Now, unstage files from the commit which we specified to edit:

```shell
git reset HEAD^
```

and verify that `b` and `c` have been unstaged with:

```shell
git status --short
```

which will output:

```text
?? b
?? c
```

Now, let's commit these two files seperately:

```shell
git add b
git commit -m "added b"

git add c
git commit -m "added c"
```

and finalize our rebase with

```shell
git rebase --continue
```

Finally, we can see our re-written history with `git log --online` which will output:

```text
74f547e (HEAD -> main) added d
6933d07 added c
dde96bf added b
26fe748 added a
```

(back to [Table of Contents](#table-of-contents))

Hope this tutorial helped you!