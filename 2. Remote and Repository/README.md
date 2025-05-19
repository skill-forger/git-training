# Module 02: Remote and repository

## Table of Contents
<ol>
    <li><a href="#objectives">Objective</a></li>
    <li><a href="#what-is-a-repository">What is a repository?</a></li>
    <li><a href="#what-is-remote">What is remote</a></li>
    <li><a href="#setup-ssh-key">Setup ssh key</a></li>
    <li><a href="#cloning-an-existing-repository">Cloning an existing repository</a></li>
    <li><a href="#setup-new-repository">Setup new repository</a></li>
</ol>

## Objectives
The objective is to learn how to initialize and manage a Git repository. 
It aims to help developers understand the fundamentals of creating a repository, 
linking it to a remote service (such as GitHub, GitLab, or Bitbucket).

## What is a repository?
A Git repository (repo) is a directory that contains the entire history of changes for a project. 
It includes all files, directories, and commit history.

**Types of repositories in Git:**

- Local Repository: A repo stored on your personal computer, where you make changes before pushing them to a remote repository.

- Remote Repository: A repo hosted on a remote server (e.g., GitHub, GitLab, Bitbucket), where the official version of the project is stored.

## What is remote?
A remote repository is a version of your repository hosted on a remote server. 
It allows team members to collaborate on the same project by sharing source code.

## Setup ssh key
### 1. Generate an SSH Key on Mac and Linux
1. execute the following to begin the key creation
    ```bash
    $ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
    ```
2. Type the default file location and replace `id_rsa` with your custom key name
    ```bash
    > Enter a file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]
    ```
3. Passphrase
    ```bash
    > Enter passphrase (empty for no passphrase): [Type a passphrase]
    > Enter same passphrase again: [Type passphrase again]
    ```

### 2. Adding a new SSH key to your GitHub account

https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account

## Cloning an existing repository
```bash
git clone git@github.com:skill-forger/git-training.git
```
Structure
- HOSTNAME: github.com
- Owner User: skill-forger
- Repo name: git-training

## Setup new repository
1. Create a new git repository
    ```bash
    git init
    ```
2. Add a remote repo url
    ```bash
    git remote add origin git@github.com:github/training-kit.git
    ```
