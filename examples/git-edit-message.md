# Example: Editting a Commit Message

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

Back to [Table of Contents](../README.md#table-of-contents)
