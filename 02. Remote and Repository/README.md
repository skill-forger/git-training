# Module 02: Remote and repository

## Table of Contents

<ol>
    <li><a href="#overview">Overview</a></li>
    <li><a href="#objectives">Objective</a></li>
    <li><a href="#what-is-a-repository">What is a repository</a></li>
    <li><a href="#what-is-remote">What is remote</a></li>
    <li><a href="#setup-ssh-key">Setup ssh key</a></li>
    <li><a href="#cloning-an-existing-repository">Cloning an existing repository</a></li>
    <li><a href="#setup-new-repository">Setup new repository</a></li>
</ol>

## Overview

This module explains the fundamentals of Git repositories and remotes—what they are, how they differ (local vs. remote),
and how they enable collaboration. Learners will generate and add SSH keys for secure access, clone an existing
repository, and initialize a new repository before linking it to a remote on a platform like GitHub. By the end, they
will understand the core workflow for creating, connecting, and collaborating with Git.

## Objectives

The objective is to learn how to initialize and manage a Git repository.
It aims to help developers understand the fundamentals of creating a repository,
linking it to a remote service (such as GitHub, GitLab, or Bitbucket).

## What is a repository

A Git repository (repo) is a directory that contains the entire history of changes for a project.
It includes all files, directories, and commit history.

**Types of repositories in Git:**

- **Local Repository**: A repo stored on your personal computer, where you make changes before pushing them to a remote
  repository.

- **Remote Repository**: A repo hosted on a remote server (e.g., GitHub, GitLab, Bitbucket), where the official version
  of
  the project is stored.

## What is remote repository

A remote repository is a version of your repository hosted on the internet or a network (remote server).
It allows team members to collaborate on the same project by sharing source code.

### Understand the analogy

Think of a standard Google Doc vs. a Microsoft Word file on your desktop.

- **Local Repository**: The Word file on your desktop. You can save changes, but no one else sees them until you email
  the file.

- **Remote Repository**: The Google Doc in the cloud. It acts as the "central source of truth." Everyone syncs their
  changes to this single location so the whole team is looking at the same document.

### Why do we need them?

You can use Git entirely on your own computer, but you need a Remote Repository for three main reasons:

- **Collaboration**: It is the meeting point for code. You push your code there; your teammates pull code from there.
- **Backup**: If your laptop breaks or gets stolen, your code is safe on the remote server.
- **Deployment**: Most modern software is "deployed" (put onto a live website/app) directly from the remote repository.

### The big three providers

While you can host a remote repository on your own private server, most developers use a hosting service.
The three most popular are:

- [GitHub](https://github.com): The most popular, home to open source.
- [GitLab](https://about.gitlab.com): Popular for DevOps and internal corporate tools.
- [Bitbucket](https://bitbucket.org): Often used by teams using Jira and Atlassian tools.

### Key terminology

1. **Origin**
   When you clone a repository or connect a local folder to a remote one, Git automatically gives that remote the
   nickname `origin`. It is just a shorthand alias for the long URL (e.g., https://github.com/username/project.git).
   You can name it anything (like `backup` or `production`),
   but `origin` is the universal standard for the primary remote.

2. **Upstream**
   If you "Fork" a project (copy someone else's repo to your account),
   the original repo is often called upstream, and your copy is called origin.

3. **Remote Tracking Branch**
   A read-only reference in your local `.git` folder that represents the state of the remote branch the last time you
   connected. You cannot edit this branch directly. It only moves when you run git fetch or git pull

## Setup SSH key

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

### 1. Using HTTPS

HTTPS (HyperText Transfer Protocol Secure) is the secure version of HTTP.
It encrypts communication between your computer and a server using TLS/SSL (Transport Layer Security/ Secure Sockets Layer), ensuring data cannot be read or modified during transfer.

**How it works**
- Git communicates over the HTTPS protocol
- You authenticate using a GitHub Personal Access Token (PAT) when pushing
- No SSH keys required

| Pros                                      | Cons                                                                         |
|-------------------------------------------|------------------------------------------------------------------------------|
| Works in most cases                       | Push operations require entering a Personal Access Token (PAT) unless cached |
| Good option for beginners                 | Managing multiple accounts is harder than with SSH                           |
| No SSH key setup needed                   | Less convenient for frequent use                                             |
| Good for read-only access or quick clones | Tokens must be stored securely                                               |

### 2. Using SSH
SSH (Secure Shell) is a cryptographic network protocol used to securely access and manage remote systems. SSH ensures confidentiality and integrity through strong cryptography.

**How it works**
- Git uses SSH (Secure Shell) to authenticate
- Authentication is done with your SSH keypair (private + public key)
    - Public and private keys are a pair in asymmetric cryptography
    - Public key encrypts data or verifies signatures and is shared openly, while the private key decrypts data or creates signatures and must remain secret, used by its owner to unlock what the public key locks, enabling secure communication and digital transactions like those in crypto or secure websites (SSL/TLS)
- Generate a key pair: [Setup SSH key](#setup-ssh-key)
    - Private key (stored on your machine)
    - Public key (uploaded to GitHub)
- When you connect, GitHub verifies that you have the correct private key
- It matches the public key stored in your GitHub account
- No passwords or tokens required during pushes


| Pros                                                        | Cons                                        |
|-------------------------------------------------------------|---------------------------------------------|
| No need to enter password/token each push                   | Requires SSH key setup                      |
| Secure authentication                                       | Some corporate networks block SSH (port 22) |
| Easy to manage multiple GitHub accounts via `~/.ssh/config` | Can be confusing for beginners              |
| Good for automation (scripts, CI/CD)                        | Must manage keys properly                   |

### 3. Using HTTPS vs SSH — Use Case Comparison

| Use Case                 | HTTPS                      | SSH                         |
|--------------------------|----------------------------|-----------------------------|
| Beginner-friendly        | Yes                        | Requires more setup         |
| Works behind firewalls   | Yes (port 443)             | Sometimes blocked (port 22) |
| Daily development        | Not too inconvenient       | Better choice               |
| Multi-account management | Harder with tokens         | Easy via `~/.ssh/config`    |
| Security                 | High                       | Very high                   |
| Quick clone / read-only  | Yes                        | Yes                         |


### 4. Clone repository using SSH
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
