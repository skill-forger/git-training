# Module 03: Branching

## Table of Contents

<ol>
    <li><a href="#overview">Overview</a></li>
    <li><a href="#objectives">Objectives</a></li>
    <li><a href="#branching-in-git">Branching in Git</a></li>
    <li><a href="#common-commands">Common Commands</a></li>
    <li><a href="#merging-branch">Merging Branch</a></li>
    <li><a href="#exercises">Exercises</a></li>
</ol>

## Overview

Git’s branching model as its “killer feature,” and it certainly sets Git apart in the VCS community.
Branching means you diverge from the main line of development
and continue to do work without messing with that main line
Git branches is incredibly lightweight, making branching operations nearly instantaneous,
and switching back and forth between branches generally just as fast.
Git encourages workflows that branch and merge often, even multiple times in a day.
Understanding and mastering this feature gives you a powerful
and unique tool and can entirely change the way that you develop

## Objectives

- Understand Git branching concepts, including how branches represent independent lines of development and how history is tracked via commit references.
- Visualize and reason about parallel development and how branching keeps `main` stable.
- List and inspect branches, including local and remote branches (`git branch`, `git branch -a`).
- Create, switch, and rename branches (`git branch <name>`, `git checkout -b <name>`, `git checkout <name>`, `git branch -m <new_name>`).
- Safely and forcefully delete branches (`git branch -d <name>`, `git branch -D <name>`).
- Synchronize branch information from remotes (`git fetch --all`).
- Merge branches and interpret outcomes, including merge commits and their parent relationships.
- Differentiate and apply fast-forward vs. 3-way merges, and understand when each occurs.
- Use `git status` to identify and manage merge states.
- Detect, inspect, and resolve merge conflicts in files.
- Leverage `git rebase` to facilitate fast-forward merges in appropriate workflows.
- Summarize and communicate branching workflows effectively (presentation exercise).

Summary: Created a concise, structured objectives list derived from `git-training/03. Branching/README.md`.

## Branching in Git

A branch in Git represents an independent line of development.
Branches serve as an abstraction for the edit/stage/commit process.
You can think of them as a way to request a brand new working directory, staging area, and project history.
New commits are recorded in the history for the current branch, which results in a fork in the history of the project.

![branching-visualization.svg](./images/branching-visualization.svg)
The diagram above visualizes a repository with two isolated lines of development, one for a little feature,
and one for a longer-running feature. By developing them in branches,
it’s not only possible to work on both of them in parallel,
but it also keeps the main branch free from questionable code.

The implementation behind Git branches is much more lightweight than other version control system models.
Instead of copying files from directory to directory, Git stores a branch as a reference to a commit.
In this sense, a branch represents the tip of a series of commits—it's not a container for commits.
The history for a branch is extrapolated through the commit relationships.

## Common Commands

- List all branches in your repository
  ```bash
  git branch
  ```
- Create a new branch
  ```bash
  git branch <branch_name>
  ```
- Create a new branch and checkout to that branch
  ```bash
  git checkout -b <branch_name>
  ```
- Switch to a branch
  ```bash
  git checkout <branch_name>
  ```
- Safe delete a branch
  ```bash
  git branch -d <branch_name>
  ```
- Hard delete a branch
  ```bash
  git branch -D <branch_name>
  ```
- Rename a branch
  ```bash
  git branch -m <branch_name>
  ```
- List all branch (including branches from remote)
  ```bash
  git branch -a
  ```
- Sync all branches and changes from remote
  ```bash
  git fetch --all 
  ```

## Merging Branch

Merging is Git's way of putting a forked history back together again.
The **git merge** command lets you take the independent lines of development
created by git branch and integrate them into a single branch.

### How it works

**Git merge** will combine multiple sequences of commits (branches) into one unified history.
**Git merge** takes two commit pointers, usually the branch tips, and will find a common base commit between them.
Once Git finds a common base commit it will create a new "merge commit"
that combines the changes of each queued merge commit sequence.

Current state of the git repository before merging:
![git-merge-before.png](./images/git-merge-before.png)

Invoking `git merge` command will merge the specified branch feature into the current branch.
Merge commits are unique against other commits in the fact that they have two parent commits
![git-merge-after.png](./images/git-merge-after.png)

### Fast Forward Merge

A fast-forward merge can occur when there is a linear path from the current branch tip to the target branch.
Instead of “actually” merging the branches, all Git has to do to integrate the histories is move (i.e., “fast forward”)
the current branch tip up to the target branch tip. This effectively combines the histories,
since all the commits reachable from the target branch are now available through the current one.
![git-merge-after.png](./images/fast-forward-merge.svg)

A fast-forward merge is only possible if the branches have not diverged.
This merging strategy is mostly for small features or bug fixes when the branch is short-lived and small in commit size.
When there is not a linear path to the target branch, Git has no choice but to combine them via a 3-way merge.
Developers can facilitate fast-forward merge via `git rebase` command to ensure branches never diverged before merging.

### 3-way Merge

When a fast-forward merge is not possible or the branches have diverged,
Git has no choice but to combine them via a 3-way merge
3-way merges use a dedicated commit to tie together the two histories.
The nomenclature comes from the fact that Git uses three commits to generate the merge commit:
the two branch tips and their common ancestor.
![3-way-merge.svg](./images/3-way-merge.svg)

For most workflows, new-feature would be a much larger feature that took a long time to develop,
which would be why new commits would appear on main in the meantime.
In this case, 3-way merges is ideal for the integration of longer-running features thanks to the fact that
the resulting merge commit serves as a symbolic joining of the two branches (integration of feature)

### Merge Conflict

When the two branches you're trying to merge both changed the same part of the same file,
Git won't be able to figure out which version to use.
When such a situation occurs, it stops right before the merge commit so that you can resolve the conflicts manually.
Using `git status` command can help to identify the current state of conflict

```bash
$ git status
On branch main
You have unmerged paths.
(fix conflicts and run "git commit")
(use "git merge --abort" to abort the merge)

Unmerged paths:
(use "git add <file>..." to mark resolution)

both modified:   merge.txt
```

Example of a merge conflict

```bash
here is some content not affected by the conflict
<<<<<<< main
this is conflicted text from main
=======
this is conflicted text from feature branch
>>>>>>> feature branch;
```

## Exercise

1. Practice Git branch common commands
2. Prepare a presentation to summarize and demonstrate the knowledge about Git Branching
3. Extra reading: https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase