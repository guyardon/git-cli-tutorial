
# Example: Staging and Committing Changes

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
