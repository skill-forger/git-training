# Week 1: Basic commands

## Required command

### 1. `git init`

### *Description*

*Create empty Git repo in specified directory. Run with no
arguments to initialize the current directory as a git repository.*

### *Usage*

```sh
git init
```

---

### 2. `git clone`

### *Description*

*The **`git clone`** command is used to create a copy of an existing repository from a remote source.*

### *Usage*

```sh
git clone <repository-url>
```

### *Example*

```sh
git clone https://github.com/user/repository.git
```

---

## 3. `git add`

### *Description*

*The **`git add`** command adds changes in the working directory to the staging area.*

### *Usage*

```sh
git add <file-name>
```

*To add all changes:*

```sh
git add .
```

### *Example*

```sh
git add index.html
```

---

## 4. `git status`

### *Description*

*The **`git status`** command shows the state of the working directory and the staging area.*

### *Usage*

```sh
git status
```

### *Example*

```sh
git status
```

---

## 5. `git commit`

### *Description*

*The **`git commit`** command saves changes to the local repository.*

### *Usage*

```sh
git commit -m "Commit message"
```

### *Example*

```sh
git commit -m "Fixed bug in authentication module"
```

---

## 6. `git pull`

### *Description*

*The **`git pull`** command fetches changes from a remote repository and merges them into the local branch.*

### *Usage*

```sh
git pull <remote> <branch>
```

*If you are on the correct branch:*

```sh
git pull
```

### *Example*

```sh
git pull origin main
```

---

## 7. `git push`

### *Description*

*The **`git push`** command uploads local commits to a remote repository.*

### *Usage*

```sh
git push <remote> <branch>
```

### *Example*

```sh
git push origin main
```

---

## 8. `git checkout`

### *Description*

*The **`git checkout`** command is used to switch branches or restore files.*

### *Usage*

*To switch branches:*

```sh
git checkout <branch-name>
```

*To create and switch to a new branch:*

```sh
git checkout -b <new-branch-name>
```

### *Example*

```sh
git checkout feature-branch
```

---

## 9. `git rebase`

### *Description*

*The **`git rebase`** command is used to apply changes from one branch onto another.*

### *Usage*

```sh
git rebase <branch-name>
```

### *Example*

```sh
git rebase main
```

*To interactively edit commits:*

```sh
git rebase -i HEAD~3
```
---

## Optional command

## 1. `git stash`

### *Description*
The **`git stash`** command temporarily stores uncommitted changes to allow work on another branch without losing modifications.

### *Usage*

```sh
git stash
git stash list
git stash apply
```
---

## 2. `git reset`

### *Description*
The **`git reset`** command is used to undo changes in a repository.

### *Usage*

```sh
git reset <commit>
```
```sh
git reset --soft HEAD~1
```
```sh
git reset --hard HEAD~1
```
### *Example*

```sh
git reset --hard origin/main
```
---

## 3. `git cherry-pick`

### *Description*
The **`git cherry-pick`** command applies a specific commit from another branch to the current branch.
### *Usage*

```sh
git cherry-pick <commit hash>
```
### *Example*

```sh
git cherry-pick a1b2c3d
```
---

## 3. `git log`

### *Description*
The **`git log`** command displays the commit history of the repository.
### *Usage*

```sh
git log
```
Show log in a single-line format:
```sh
git log --oneline
```
### *Example*

```sh
git log --oneline --graph --decorate
```
---

