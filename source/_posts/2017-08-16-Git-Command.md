---
title: 2017-08-16-Git-Command
date: 2017-08-16 22:45:12
tags:
categories: Git Notes
---

| Command | Comment |
| ------- | ------- |
| git init | |
| git status | See what the current state of our project is. |
| git add . | Stage new and modified files, without deleted files. |
| git add -u | Stage deleted and modified files, without new files. |
| git add -A | Stage new, deleted and modified files. |
| git rm `file name` | |
| git commit -m `msg` | |
| git log | A journal that remembers all the changes we've commited so far. |
| git remote add origin `repo address` | |
| git push -u origin master | The '-u' tells Git to remember the parameters so that we can simply run 'git push' and Git will know what to do. |
| git pull origin master | |
| git diff HEAD/--staged | |
| git reset `file name` | Unstage files. |
| git branch | |
| git branch -r | Check remote branch. |
| git branch `branch name` | Create a new branch. |
| git branch -d `branch name` | Delete a branch. |
| git checkout `branch name` | Checkout the new branch. |
| git checkout -b `branch name` | Create and checkout the new branch. |
| git checkout -b `local branch name` origin/`remote branch name` | |
| git merge `branch name` | |
| git reset --hard `commit id` | Back to some commit version. |
