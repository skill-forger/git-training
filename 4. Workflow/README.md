# Week 4: Workflow

## Table of Contents

<ol>
    <li><a href="#objectives">Objectives</a></li>
    <li><a href="#feature-branch-workflow">Feature Branch Workflow</a></li>
    <li><a href="#gitflow-workflow">Gitflow Workflow</a></li>
    <li><a href="#forking-workflow">Forking Workflow</a></li>
    <li><a href="#exercises">Exercises</a></li>
</ol>

## Overview

Git is the most widely used version control system, offering flexibility in managing changes.
Since there is no standard Git workflow, teams should agree on a consistent process for applying changes.
Adopting a well-defined Git workflow ensures efficiency and collaboration.
Several established Git workflows can help teams work effectively.

## Objectives

- Understand the description and basic usage for each Git workflow
- Compare the differences between one workflow and another
- Practice Gitflow and Forking workflow

## Feature Branch Workflow

The core idea behind the Feature Branch Workflow is that all feature development
should take place in a dedicated branch instead of the main branch.
This encapsulation makes it easy for multiple developers to work on a particular feature
without disturbing the main codebase. It also means the main branch will never contain broken code,
which is a huge advantage for continuous integration environments.

### How it Works

The Feature Branch Workflow uses a central repository where main represents the official project history,
and developers create a new branch for each feature instead of committing directly to main.
These branches have clear, descriptive names and function the same as main,
allowing independent edits, staging, and commits.

Feature branches can also be pushed to the central repository,
enabling collaboration without affecting the official code while serving as a backup for local commits.
Since main is the only special branch, storing multiple feature branches does not cause issues,
making this workflow an efficient and organized approach to development.

### Workflow Steps

1. Start with the main branch
    ```bash
    git checkout main
    git fetch origin 
    git reset --hard origin/main
    ```
2. Create the repository
   This switches the repo to the main branch, pulls the latest commits
   and resets the repo's local copy of main to match the latest version.
3. Create a new-branch
    ```bash
    git checkout -b new-feature
    ```
4. Update, add, commit changes
    ```bash
    git status
    git add <some-file>
    git commit
    ```
5. Push feature branch with changes to remote
    ```shell
    git push -u origin new-feature
    ```
6. Resolve feedback/comment
   Teammates comment and approve the pushed commits.
   Resolve their comments locally, commit, and push the suggested changes to the Pull Request.
7. Merge your pull request
   Before you merge, you may have to resolve merge conflicts if others have made changes to the repo.
   When your pull request is approved and conflict-free, you can add your code to the main branch.

### Pull Request

Aside from isolating feature development, branches make it possible to discuss changes via pull requests.
Once someone completes a feature, they don’t immediately merge it into main.
Instead, they push the feature branch to the central server
and file a pull request asking to merge their additions into main.
This gives other developers an opportunity to review the changes before they become a part of the main codebase

Code review is a major benefit of pull requests, but they’re actually designed to be a generic way to talk about code.
You can think of pull requests as a discussion dedicated to a particular branch.
This means that they can also be used much earlier in the development process.
For example, if a developer needs help with a particular feature, all they have to do is file a pull request.
Interested parties will be notified automatically,
and they’ll be able to see the question right next to the relevant commits.

## Gitflow Workflow

Gitflow is a Git branching model that uses feature branches and multiple primary branches,
making it more structured than trunk-based development.
Introduced by Vincent **Driessen at nvie**, Gitflow involves long-lived feature branches
that require more collaboration and pose a higher risk of conflicting updates.
Developers work on feature branches and delay merging them into the main trunk until completion. \

This workflow is well-suited for projects with scheduled releases and supports continuous delivery in DevOps.
While Gitflow follows the same principles as the Feature Branch Workflow,
it assigns specific roles to branches for preparing, maintaining, and recording releases,
enabling better collaboration, pull requests, and isolated experiments.

### How it Works

Instead of a single **main** branch, this workflow uses two branches to record the history of the project.
The **main** branch stores the official release history,
and the **develop** branch serves as an integration branch for features.
It's also convenient to tag all commits in the main branch with a version number.

![git-flow-how-it-works.svg](./images/git-flow-how-it-works.svg)

The **develop** branch will contain the complete history of the project,
whereas **main** branch will contain an abridged version.
Other developers should now clone the central repository and create a tracking branch for develop.

### Feature Branches

Each new feature should reside in its own branch yet, instead of branching off of **main**,
feature branches use **develop** as their parent branch.
When a feature is complete, it gets merged back into **develop**.
Features should never interact directly with **main**.
Feature branches are generally created off to the latest **develop** branch.

![git-flow-feature-branches.svg](./images/git-flow-feature-branches.svg)

- Creating a feature branch
    ```bash
    git checkout develop
    git checkout -b feature_branch
    ```
- Finishing a feature branch
    ```bash
    git checkout develop
    git merge feature_branch
   ```

### Release Branches

Once **develop** has acquired enough features for a release (or a predetermined release date is approaching),
you fork a **release** branch off of **develop**.
Creating this branch starts the next release cycle, so no new features can be added after this point—only bug fixes,
documentation generation, and other release-oriented tasks should go in this branch.

![git-flow-release-branches.svg](./images/git-flow-release-branches.svg)

Once it's ready to ship, the release branch gets merged into **main** and tagged with a version number.
In addition, it should be merged back into **develop**, which may have progressed since the release was initiated.

- Creating a **release** branch
    ```bash
    git checkout develop
    git checkout -b release/0.1.0
    ```
- Finish a **release** branch
    ```bash
    git checkout main
    git merge release/0.1.0
    ```

### Hotfix Branches

Maintenance or **hotfix** branches are used to quickly patch production releases.
**Hotfix** branches are a lot like **release** branches and **feature** branches
except they're based on **main** instead of **develop**.
This is the only branch that should fork directly off of **main**.
As soon as the fix is complete, it should be merged into both **main** and **develop** (or the current **release**
branch),
and main should be tagged with an updated version number.

![git-flow-how-it-works.svg](./images/git-flow-how-it-works.svg)

Having a dedicated line of development for bug fixes lets your team address issues
without interrupting the rest of the workflow or waiting for the next release cycle.
You can think of maintenance branches as ad hoc **release** branches that work directly with **main**

- Creating a **hotfix** branch
    ```bash
    git checkout main
    git checkout -b hotfix_branch
    ```
- Finish a **hotfix** branch
    ```bash
    git checkout main
    git merge hotfix_branch
    git checkout develop
    git merge hotfix_branch
    git branch -D hotfix_branch
    ```

## Forking Workflow

The Forking Workflow is fundamentally different from other popular Git workflows.
Instead of using a single server-side repository to act as the “central” codebase.
This means that each contributor has not one, but two Git repositories: a private local one and a public server-side
one.
The Forking Workflow is most often seen in public open source projects.

The main advantage of the Forking Workflow is that contributions can be integrated
without the need for everybody to push to a single central repository.
Developers push to their own server-side repositories,
and only the project maintainer can push to the official repository.
This allows the maintainer to accept commits from any developer without giving them write access to the official
codebase.

### How it Works

The Forking Workflow starts with an official public repository stored on a server, similar to other Git workflows.
However, instead of cloning the official repository directly,
a developer forks it, creating a personal copy on the server.
This fork acts as their own public repository, where they have full control, while others can only pull changes from it.
The developer then clones this forked repository to their local machine,
creating a private development environment for making changes.

When the developer is ready to share their work,
they push commits to their personal repository instead of the official one.
To request merging their changes into the main repository, they submit a pull request, notifying the project maintainer.
This pull request also serves as a discussion platform for reviewing and addressing any issues with the contributed
code.

### Workflow Steps

1. A developer 'forks' an 'official' server-side repository. This creates their own server-side copy.
2. The new server-side copy is cloned to their local system.
3. A Git remote path for the 'official' repository is added to the local clone.
4. A new local feature branch is created.
5. The developer makes changes on the new branch.
6. New commits are created for the changes.
7. The branch gets pushed to the developer's own server-side copy.
8. The developer opens a pull request from the new branch to the 'official' repository.
9. The pull request gets approved for merge and is merged into the original server-side repository

### Fork a Repository

It's important to note that "forked" repositories and "forking" are not special operations.
Forked repositories are created using the standard git clone command

All new developers to a Forking Workflow project need to fork the official repository.
As previously stated, forking is just a standard git clone operation.
It’s possible to do this by SSH’ing into the server and running git clone to copy it to another location on the server

Forking Workflow requires two remotes—one for the official repository,
and one for the developer’s personal server-side repository.
A common convention is to use origin as the remote for your forked repository
(this will be created automatically when you run git clone) and upstream for the official repository.

```bash
git remote add upstream https://github.com/maintainer/repo
git remote add upstream https://user@github.com/maintainer/repo.git
```

### Pull Request

![forking-flow-pull-request.svg](./images/forking-flow-pull-request.svg)
Once a developer is ready to share their new feature, they have to make their contribution accessible
to other developers by pushing it to their public repository.

```bash
git push origin feature-branch
```

Then, the developers need to notify the project maintainer that they want to merge their feature into the official
codebase.
the project maintainer may proceed with the review process and merge into the official repository.

## Exercises

1. Create a repository and practice the Gitflow Workflow
2. Prepare a presentation to summarize and demonstrate the knowledge about Git workflow
3. Extra reading: https://www.atlassian.com/git/tutorials/comparing-workflows