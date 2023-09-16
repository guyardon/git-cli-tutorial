# Example: Splitting a Commit to Multiple Commits

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
