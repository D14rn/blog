+++
date = '2024-11-24T17:10:16+01:00'
draft = true
title = 'Quick Git Commands'
+++

## Introduction
In this post, I will show some basic git commands.

## Commands

### git commit
This one of the most important commands in git, it's used to create a commit.
Using it without any flags will open the text editor, making it easy to write a detailled description of the commit.

```vim
> git commit
# Your branch is up to date with 'origin/main'.
#
# Changes to be committed:
#       new file:   content/posts/quick-git-commands.md
#
This is the commit's message that explains the changes briefly

This is the commit's description that explains the changes it brings.
You can write on multiple lines what was done and why it was done.
```

```
> git log
commit 4f5c8b76e880f0fe7e18f0bd1fe860c843ea12da (HEAD -> main)
Author: D14rn <49399494+D14rn@users.noreply.github.com>
Date:   Sun Nov 24 17:16:02 2024 +0100

    This is my commit message that explains the changes briefly

    This is my commit description that explains the changes made
    I can write in multiple lines what I did and why I did it
```

### git commit --amend
This one is useful whenever you realize you made a (small) mistake after creating a commit, it enables you to add staged files to the previous commit, but also enables you to simply modify the commit's message/description. This modification replaces the old commit with a new one, so be careful.

#### Changing the commit message/description
```bash
# opens the editor (recommended if you want to add a description or modify it)
git commit --amend
# doesn't
git commit --amend -m "your new commit message"
```

#### Adding changes to the previous commit
```bash
# you stage some changes and commit them
git add README.md
git commit -m "chore: fix typo in readme"

# you fixed a typo you made while fixing the previous typo
git add README.md
# keep the previous commit's message
git commit --amend --no-edit
```

### git reset
The `git reset` command allows you to move your repository back to a previous state, almost like going back in time.
However, be careful when using this command, as it can be very destructive (see `git reflog` for recovering "lost" changes).

There are three modes you can use:
- `git reset --soft`
- `git reset --mixed`
- `git reset --hard`

I will assume that you know and understand Git's three zones (working directory, staging area/index, repository).

#### git reset --hard
This mode resets all three zones back to their state at the specified commit, effectively discarding all the modifications you currently have.

A common variations of this command is:
```bash
# reset everything back to state of the previous commit
git reset --hard HEAD^1
# or
git reset --hard HEAD^
```
Note: you can also use `HEAD^1` with the other modes, as it's essentially a reference to a commit.

#### git reset --mixed (default)
This is the default `git reset` mode. It will move the current branch pointer to the specified commit and reset the staging area, but it will keep the working directory intact.
You can use this mode if you made a commit by mistake and want to go back while also keeping your current changes.

#### git reset --soft
This is the "safest" `git reset` option, it will only move the current branch pointer, keeping the staging area and working directory untouched.

### git push --set-upstream
Also usable as `git push -u`, this command "pushes" a local branch to a remote repository.

```bash
# We make the local branch available to the repository at 'origin'
# in the remote branch 'feature_branch'
git push -u origin feature_branch
```

### 