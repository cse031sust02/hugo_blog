---
date: "2017-04-11T11:11:48+06:00"
title: "My Personal Git Cheat Sheet"
---

---

## What is GIT?
Git is a free and open source distributed version control system.

**Why we use VCS (version control system)?**

- Code Revision
- Like a Time Machine
- Multiple Developer

**Why GIT (among other VCS)?**

- Can work locally without any central server

---

## Setup
Now let's install Git on our machine and start using it.


### Installation
Please follow the [offical doc](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) to install git.

### Configuration
Use **`git config`** command to get and set configuration variables 

**Config file locations**  :

* `--system` : configuaration for every user on the system(OS) and all their repositories.
* `--global` : configuarations specific to your user. (OS user)
* `--local` : configuarations for current repository.


**Set Config**

```bash
git config --global user.name "John Doe"
git config --global user.email "johndoe@example.com"
```

**Get Config**

```bash
git config --list
git config --global --list
git config --system --list
```

### Initialization (create a new repository)
To initialize git on a project, simply use `git init` command.
( *a hidden folder named `.git` will be created in the project's root directory* )

To get a copy of an existing Git repository, use the `git clone` command.

---

## Extra

> - [What's Inside .git Directory?](http://gitready.com/advanced/2009/03/23/whats-inside-your-git-directory.html)
> - **Editor** : By default, Git uses whatever you’ve set as your default text editor ($VISUAL or $EDITOR) or else falls back to the vi editor to create and edit your commit and tag messages.for example, to use Sublime as the editor, `git config --global core.editor "subl -n -w"`
> - **aliases** : we can also easily set up an alias for each command using git config.

---

## Lifecycle

![Lifecycle](https://git-scm.com/book/en/v2/book/02-git-basics/images/lifecycle.png)

**source** : *https://git-scm.com/book/en/v2/book/02-git-basics/images/lifecycle.png*

Files has mainly 4 statuses :

### 1. **untracked** : 
at first any new file is untracked.

- **-->** use `git add` command to stage the file

### 2. **staged** :
after we use 'git add' command, the file is statged.

- **-->** use `git commit` command to commit the staged file
- **<--** use `git reset HEAD` command to unstage that file

### 3. **unchanged** : 
If the file is not changed since its last commit, the file is unchanged.

### 4. **unstaged** : 
If there is any modification to that staged or unchanged file, that file becomes unstaged.

- **-->** again use `git add` command to stage that file
- **<--** use `git checkout` command to discard changes

> note : 'git checkout' is a dangerous command! Use stash instead.

---

## Basic Commands

The diagram below show how the git works locally and remotely using different commands.

![Commands](http://images.osteele.com/2008/git-transport.png)

**source** : *http://blog.osteele.com/2008/05/my-git-workflow/*

I found this [video](https://www.youtube.com/watch?v=3a2x1iJFJWc) really useful to understand  the workflow.

### git add
Use `git add` command to track the untracked files (put it on the stage).
  
- add single file : `git add file.ext`
- add all files : `git add .` or `git add -A` . ([Difference?](http://stackoverflow.com/questions/572549/difference-between-git-add-a-and-git-add))


### git commit
Commits the staged snapshot to the project history.

Different ways to commit,

- **commit all staged files** : 

```
git commit
```

This will open an editor, write your commit message and exit. To write the commit message directly in command line, use the `-m` flag. e.g, `git commit -m "My Commit Message"`


- **commit all staged and unstaged files** : 

```
git commit -am "commit message"
```
  
when we use '-a' flag, it includes all changed files. Git will automatically stage every unstaged files before doing the commit. note that, untracked files will not be commited using this command.

- commit single file :  `git commit -m "commit message" FILE_NAME`
- commit multiple files : `git commit -m "commit message" FILE1, FILE2..`
- ammend the previous commit : `git commit --amend`

e.g,
```bash
git commit -m 'initial commit'
git add forgotten_file
git commit --amend
```

> **do not use `--amend' if you already pushed your commit.*


### git log
Show commit logs

use `git log` command to show all the commits from the very beginning (for currently active branch).

e.g,

```bash
commit 1cddaa29ad059a6083e776cc3e4b950e6487f236
Author: Talha Ibne Imam <talha@bscheme.com>
Date:   Sat Apr 22 12:26:11 2017 +0600

    Registration Complete

commit eea5997a17f02e78d78ccf69a233123192a73822
Author: Talha Ibne Imam <talha@bscheme.com>
Date:   Thu Apr 20 14:13:18 2017 +0600

    Design Complete

commit 178d3c00a5e55cd0f6ba0170a9dd58dda24561cf
Author: Talha Ibne Imam <talha@bscheme.com>
Date:   Thu Apr 20 11:35:36 2017 +0600

    First Commit

```

There are many different options avalaible for showing logs in different ways. 

for example,

- Most recent commits : `git log -3` (last 3 commits)
- Show commits in one line : `git log --pretty=oneline`
- Show commits for a specific file : `git log test.txt`
- Show commits by any specific author : `git log --author=talha`
- Show in a pretty format : `git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative` [*src : [Coderwall](https://coderwall.com/lordmonkey/comments)*]

for more details, please use the command `git log --help`.


### git show :
Shows the changes of a particular commit

```bash
git show COMMIT_HASH*
```

> **only first 4-5 character of COMMIT_HASH is enough!* [(or not?)](https://stackoverflow.com/questions/34764195/how-does-git-create-unique-commit-hashes-mainly-the-first-few-characters)

If we do not specify COMMIT_HASH, then it will show changes from HEAD. (HEAD is a reference to the last commit in the currently checked-out branch.)

'git show' can be used to show other objects rather than commits. such as tags, trees etc. for more details, please visit [official link](https://git-scm.com/docs/git-show)

### git diff:
Show changes between commits, commit and working tree, etc

we usually use the `git status` command to see which files were currently changed. To understand how they were changed in detail, we can use `git diff`.
  
**`git diff`** 

show changes only that are unstaged.

- all unstaged files : `git diff`
- single unstaged file : `git diff FILENAME`
- multiple unstaged file : `git diff FILE1 FILE2`

**`git diff --staged`**

show changes only that are staged.
  
- all staged files : `git diff --staged`
- single staged file : `git diff --staged FILENAME`
- multiple staged file : `git diff --staged FILE1 FILE2`

> we can use `--cached` instead of `--staged` (`--staged` is a synonym of `--cached`).


**`git diff HEAD`** 

show changes that are tracked (staged + unstaged).

---

## Working Remotely

### git remote:
Manage repositories

To collaborating with other developers, we need to manage remote repositories and pushing and pulling data to and from.
  
- show list with names : `git remote -v`
- add new remote : `git remote add [remote-name] <url>`
- update a remote's url: `git remote set-url [remote-name] [new-url]`
- remove a remote : `git remote rm [remote-name]`

### git push:
Push commits to remote repository

After we made some commits, we might want to push them to a remote repository. this can be done with a `git push [remote-name] [branch-name]` command. ie, `git push origin master`

### git pull:
Fetch and merge remote changes.

perform a pull can be done simply with a ` git pull` command.


> ### 'git fetch'  vs  'git pull' :
> In its default mode, `git pull` is shorthand for `git fetch` followed by `git merge FETCH_HEAD`. src : https://git-scm.com/docs/git-pull

> more details : http://stackoverflow.com/a/7104747/7804179