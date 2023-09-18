# Example: Initializing a Git Repository

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

The .git folder is a hidden directory that Git uses to store all the information and metadata about a Git repository, including project history, commits, configuration files, etc. It is located at the root of the repository and is critical for the functioning of Git.

To see the status of our current Git repository, can use `git status` which will output the following:

```text
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

We can see that Git is initialized, and we are on a branch called main.

We can introduce ourselves to Git for the first time by setting our user name and email, which will appear on commit logs:

```shell
git config --global user.name Guy Ardon
git config --global user.email guyardon@gmail.com
```

We can see all our configurations via the `git config --list` command.

Back to [Table of Contents](../README.md#table-of-contents)
