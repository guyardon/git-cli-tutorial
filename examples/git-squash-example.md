
# Example: Squashing Commits

Let's initialize our repository in the home `~` directory, and create three files `a`, `b` and `c` in 3 seperate commits:

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

We'll enter the interactive rebase menu with

```shell
git rebase -i --root
```

The first few lines will show:

```text
pick 766f449 my first commit
pick 6106de8 my second commit
pick 94bfe32 my third commit
```

we'll change the `pick` prefix in the last two commits to `squash`:

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

Here we can edit the message for the squashed commit. Let's delete the existing text and write:

```text
adding files a, b and c
```

Then save and quit (`esc + :wq`).

Finally `git log --oneline` will verify that the commits have been squashed:

```text
1dded2a (HEAD -> main) adding files a, b and c
```

`git status` will indicate that we are on a clean tree, and `ls` will show that all three files, `a` , `b` and `c` are present!

Back to [Table of Contents](../README.md#table-of-contents)
