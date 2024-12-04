# git Cheat Sheet

## Setup

### Set a name for version history review

```bash
git config --global user.name “[firstname lastname]”
```

---

### Set an email address associated with reviewer

```bash
git config --global user.email “[valid-email]”
```

---

### Set automatic command line coloring for Git for easy reviewing

```bash
git config --global color.ui auto
```

---

## Initialization

### Initialize an existing directory as a Git repository

```bash
git init
```

---

### Retrieve an entire repository from a hosted location via URL

```bash
git clone [url]
```

---

### Pushing a new local repo to GitHub

```shell
git init  
git add somefile  
git commit -m "initial commit"  
git remote add origin https://github.com/username/new_repo  
git push -u origin master
```

#### Editing url

```shell
git remote set-url origin https://github.com/username/new_repo_edited
```

---

## Staging

### Show modified files in working directory, staged for your next commit

```bash
git status
```

---

### Add a file as it looks now to your next commit (stage)

```bash
git add [file]
```

---

### Unstage a file while retaining the changes in working directory

```bash
git reset [file]
```

---

### Show difference of what is changed but not staged

```bash
git diff
```

---

### Show difference of what is staged but not yet commited

```bash
git diff --staged
```

---

### Commit your staged content as a new commit snapshot

```bash
git commit -m “[descriptive message]”
```

#### A note on commit messages

Effective commit messages consist of two seperatre parts

##### Subject

A brief summary of the change you made to the project

##### Body

A concise, clear description of what you did.

## Branch & Merge

### List your branches. A \* will appear next to the currently active branch

```bash
git branch
```

---

### Create a new branch at the current commit

```bash
git branch [branch-name]
```

---

### Switch to another branch and check it out into your working directory

```bash
git checkout
```

---

### Merge the specified branch’s history into the current one

```bash
git merge [branch]
```

---

### Create new branch from existing branch

#### 1. Create new branch of current branch

```shell
git checkout -b new_branch current_branch
```

#### 2. Commit changes

```shell
git commit -am "Created new_branch from current_branch"
```

#### 3. Push changes to GitHub

```shell
git push origin new_branch
```

---

## Inspect & Compare

### Show all commits in the current branch’s history

```bash
git log
```

---

### Show the commits on branchA that are not on branchB

```bash
git log branchB..branchA
```

---

### Show the commits that changed file, even across renames

```bash
git log --follow [file]
```

---

### Show the difference of what is in branchA that is not in branchB

```bash
git diff branchB...branchA
```

---

## Update

### Add a git URL as an alias

```bash
git remote add [alias] [url]
```

---

### fetch down all the branches from that Git remote

```bash
git fetch [alias]
```

---

### Merge a remote branch into your current branch to bring it up to date

```bash
git merge [alias]/[branch]
```

---

### Transmit local branch commits to the remote repository branch

```bash
git push [alias] [branch]
```

---

### Fetch and merge any commits from the tracking remote branch

```bash
git pull
```

---

## Temporarily Commit

### Save modified and staged changes

```bash
git stash
```

---

### List stack-order of stashed file changes

```bash
git stash list
```

---

### Lrite working from top of stash stack

```bash
git stash pop
```

---

### Discard the changes from top of stash stack

```bash
git stash drop
```

---

### Rename a branch

```shell
git remote rename <old-name> <new-name>
```

---

### Rename a repo

```shell
git remote set-url origin NEW_URL
```


# References

1. [git-cheat-sheet.pdf (gitlab.com)](https://about.gitlab.com/images/press/git-cheat-sheet.pdf)
2. [git-cheat-sheet-education (github.com)](https://education.github.com/git-cheat-sheet-education.pdf)
3. [Git cheat sheet | Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials/atlassian-git-cheatsheet)
4. [Git Cheat Sheet (2024) - All Git Commands (geeksforgeeks.org)](https://www.geeksforgeeks.org/git-cheat-sheet/)
5. 