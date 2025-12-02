# Module 01: Git and Version Control

## Table of Contents

<ol>
    <li><a href="#overview">Overview</a></li>
    <li><a href="#objectives">Objectives</a></li>
    <li><a href="#version-control">Understanding Version Control</a></li>
    <li><a href="#core-concepts">Core Concepts</a></li>
    <li><a href="#basic-commands">Basic Commands</a></li>
    <li><a href="#collaboration-and-open-source">Collaboration and Open Source</a></li>
</ol>

## Overview

This concise document provides a foundational introduction to **Git and Version Control Systems (VCS)**, designed to
accelerate a developer's entry into collaborative programming environments. It establishes the conceptual framework by
explaining the **Distributed VCS** architecture and defining key components like the **Repository**, **File States**,
and **Commit** history. The training then transitions to practical application, detailing essential daily **Basic
Commands** and illustrating professional collaboration methodologies, specifically the use of **Branching, Merging**,
and **Pull Requests (PRs)** to ensure safe and effective team code integration.

## Objectives

- Understand of the purpose and mechanics of * *Version Control Systems (VCS)** and the distributed nature of **Git**.
- Able to define and correctly utilize key Git concepts, including **Repository**, **File States**, and the function of
  a **Commit**.
- Perform the most common daily Git operations, such as cloning, status checking, adding, committing, pushing, and
  pulling.
- Create and switch between **merging** branches to manage isolated lines of development.
- Comprehend the professional methodology of using **Pull Requests (PRs)** to submit code for review and integrate
  changes into a shared codebase.

## Version Control

### What is Version Control (VC)?

Imagine writing a large document and saving multiple copies with names like `Final_Doc_v1`, `Final_Doc_v2_with_fixes`,
and `Final_Doc_really_final`. Now imagine a group project of 10 members doing this simultaneously, it is merely
impossible to control the version of each individual without a systematic method.

**Version Control** is born to solve this problem, it is a system that records changes to a file or set of files over
time so that you can recall specific versions later.
It's the "**undo button**" for your entire project, keeping track of *who* made *what* change and *when*.

### Version Control Systems (VCS)

There are two main types of modern VCS:

* **Centralized VCS (CVCS):** Relies on a single, central server for all file versioning operations. Developers commit
  changes directly to this central repository. (Example: Subversion/SVN). The downside is that if the central server
  goes down, no one can save or access history.
* **Distributed VCS (DVCS):** Every developer has a full copy (a **clone**) of the entire project repository, including
  its complete history, on their local machine. This is the modern, resilient standard.

### Git and GitHub

* **Git:** This is the most popular **Distributed Version Control System (DVCS)** itself. It is the core **tool** you
  install on your computer that handles the versioning logic.
* **GitHub (or GitLab, Bitbucket):** These are **hosting services** for Git repositories. They are the remote servers
  that store the official, shared copy of the code, making collaboration easy. Git is the engine; GitHub is the garage
  where you park and share your code.

## Core Concepts

### Repository (Repo)

A **Repository** is essentially a folder where Git tracks all changes.

* **Local Repository:** The copy of the project and its history stored on your computer; in other words, the working
  directory.
* **Remote Repository:** The copy of the project and its history stored on a hosting service (like GitHub) that the team
  shares.

### File States

Git tracks files in three main states, forming your basic workflow:

1. **Unstaged:** The actual files you are currently editing. These files are **modified** but not yet tracked
   for the next commit.
2. **Staged (tracked)** A temporary area where you place the changes you want to include in the *next* commit. You
   can stage individual files or specific changes within a file.
3. **Committed:** Where Git permanently stores the version history as **commits**.
4. **Pushed:** When a commit is pushed into a remote repository, usually via pull/merge request.

### Commit

A **Commit** is the fundamental unit of history in Git. It is a **snapshot** of your repository at a specific point in
time.

* Every commit has a unique identifier (a **SHA-1 hash**).
* It includes metadata like the author, date, and, most importantly, a **commit message** explaining what changes were
  made and why.
* **Best Practice:** Commit early, commit often, and write meaningful commit messages.

### Branching and Merging

* **Branch:** A branch is a lightweight, movable pointer to a commit. It allows you to create an independent line of
  development.
    * The standard main line of development is typically the **`main`** or **`master`** branch.
    * **Crucial for Teams:** You should always create a new branch (e.g., `feature/login-page`) for every feature or bug
      fix you work on. This isolates your changes from the stable code.
* **Merging:** The process of combining the changes from one branch (e.g., your feature branch) into another (e.g.,
  `main`).
* **Merge Conflict:** This happens when Git cannot automatically merge two changes because the *exact same lines* were
  modified differently in the two branches being combined. You must manually open the files and resolve the conflicts
  before completing the merge.

***

## Basic Commands

These commands represent your most common daily Git workflow:

| Command                         | Purpose                                                                                                     | Workflow Stage |
|:--------------------------------|:------------------------------------------------------------------------------------------------------------|:---------------|
| `git init`                      | Downloads a remote repository to your local machine.                                                        | Initial Setup  |
| `git clone <url>`               | Create empty Git repo in specified directory and initialize the current directory as a git repository.      | Initial Setup  |
| `git status`                    | Shows which files are modified, staged, or untracked.                                                       | Daily Check    |
| `git add <file>` or `git add .` | Moves modified files to the **Staging Area**.                                                               | Staging        |
| `git commit -m "message"`       | Records the staged changes as a permanent **commit** in your local repo.                                    | Committing     |
| `git push`                      | Uploads your local commits to the **Remote Repository** (e.g., GitHub).                                     | Sharing        |
| `git pull`                      | Downloads the latest changes from the remote repo and automatically **merges** them into your local branch. | Syncing        |
| `git log`                       | Displays the history of commits for the current branch.                                                     | Inspecting     |
| `git checkout -b <new-branch>`  | Creates a new branch and immediately switches to it.                                                        | Branching      |
| `git checkout`                  | Switches branches or restore files.                                                                         | Branching      |

***

## Collaboration and Open Source

### The Pull Request (PR) Workflow

In professional and open-source settings, you rarely push directly to `main`. Instead, you use a **Pull Request (PR)** (
or **Merge Request / MR**):

1. **Branch:** Create a new branch for your feature (`git checkout -b my-new-feature`).
2. **Commit:** Write code and commit your changes (`git add .` then `git commit`).
3. **Push:** Push your local feature branch to the remote (`git push origin my-new-feature`).
4. **Create PR:** Go to the hosting service (GitHub) and open a Pull Request, requesting that your feature branch be
   merged into `main`.
5. **Review:** Your teammates review the code, suggest changes, and ensure quality.
6. **Merge:** Once approved, the PR is merged, and your feature is integrated into the `main` branch.

### Open Source Contribution

Git and GitHub are the backbone of open-source development. To contribute to an open-source project:

1. **Fork:** Create your own copy of the project's repository on GitHub (a **fork**).
2. **Clone:** Clone your forked repository to your local machine.
3. **Branch & Commit:** Make your changes on a new branch.
4. **Pull Request:** Submit a Pull Request from your fork back to the original project's repository.
