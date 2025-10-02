# Git Initiation

## Installation

### 1. MacOS

- Install Git with Homebrew
  If you have installed Homebrew to manage packages on OS X, you can follow these instructions to install Git:

1. Open your terminal and install Git using Homebrew:
    ```bash
    $ brew install git
    ```
2. Verify the installation was successful:
    ```bash
    $ git --version
    ```

### 2. Windows

1. Download the latest [Git for Windows installer](https://git-scm.com/downloads/win).
2. Run the .exe file and follow the setup instructions.
3. Verify the installation was successful:
    ```bash
    $ git --version
    ```

### 3. Linux

1. Use your package manager to install Git. For example, on Ubuntu:
    ```bash
    $ sudo apt-get update
    $ sudo apt-get install git
    ```
2. Verify the installation was successful:
    ```bash
    $ git --version
    ```

## User Configuration

- Configure for each repository
   ```bash
   $ git config user.email "your email"
   $ git config user.name "your name"  
   ```
- Configure globally for user
   ```bash
   $ git config --global user.email "your email"
   $ git config --global user.name "your name"  
   ```
- Verify configuration
   ```bash
   $ git config user.email
   $ git config user.name
   ```

