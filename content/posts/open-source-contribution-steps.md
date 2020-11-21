---
date: "2018-09-27T11:36:51+06:00"
title: "A step-by-step technical guide for open source contribution"
---

## Intro

This is a very simple guide for first-timers to making open source contributions. I guess that you already have a GitHub account and know basic git commands.

---

## Steps for Contributing

### Fork

First, we need to choose a project we want to contribute. Then we will fork the project to our github account.

### Clone

Now, we need to clone the project to our machine from our fork.

```bash
$ git clone <url>
```

### Syncing the fork
	
We should keep our fork up-to-date with the main(aka upstream) repository. For this, we have to set up a new remote that points to the original project.

```bash
$ git remote add upstream <main-project-url>
```

So, We have two remotes now for this project on disk :

- **origin** : which points to our GitHub fork of the project. We can read and write to this remote.
- **upstream** : which points to the main project’s GitHub repository. We can only read from this remote.

Whenever we want to sync our local copy with the upstream project, we can do it with the `git pull` command.

```bash
$ git pull upstream master
```

Note that, Syncing our fork only updates the local copy of the repository. To update our fork on GitHub, we must push the changes there.

```bash
$ git push origin master
```

### Create new Branch

Before starting our work, we can create a new branch where we will commit our changes.

```bash
$ git checkout -b <your-branch-name>
```

### Work & Commit

We can now start our work. We should follow the project's CONTRIBUTING file if there is one. Whenever we are ready to commit, we will commit the changes with good commit messages).

```bash
$ git add .
$ git commit -am <commit-msg>
```

### Push
	
We will then push the changes to our fork.

```bash
git push origin <your-branch-name>
```

### Pull Request

Now, We need to make a pull request to the main repository. To do that, we can go to the repositorys page, click **'new pull request'** button and submit our pull request. For more details on pull request, please go to [this github page](https://help.github.com/articles/creating-a-pull-request-from-a-fork/).

> A pull request doesn’t have to represent finished work. We can open a pull request anytime, so that other developers can check and give feedback on the work. In that case, we should mark it as a “WIP” (Work in Progress) in the subject line.

We will then wait for getting our work approved and merged to the main repository. After ther pull request has been merged, We can delete the branch we created earlier.

> If the Pull Request was closed without being merged, GitHub will show notification about deleting unmerged commits.