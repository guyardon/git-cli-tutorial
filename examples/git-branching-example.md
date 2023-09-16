
# Example: Working with Branches

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

# Example: Merging Branches

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

# Example: Merging Conflicting Branches

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
