# Git Basics

> Joseph P. Vantassel, The University of Texas at Austin

[![License](https://img.shields.io/badge/license-CC--By--SA--4.0-brightgreen.svg)](https://github.com/jpvantassel/git-course/blob/master/Licence.md)

## Table of Contents

- [Setup/Configuration](#Setup/Configuration)
- [Need Help](#Need-Help)
- [Local Repositories](#Local-Repositories)
- [Remote Repositories](#Remote-Repositories)

## Setup/Configuration

```bash
git --version                               # Determine version number
git config --global user.name John Doe      # Set up configuration with name
git config --global user.email jd@mail.com  # Set up configuration with email
git config --list                           # Confirm and view changes
```

## Need help

```bash
git help <verb>
git <verb> --help
# For Example
git help config
git config --help
```

## Local Repositories

```bash
cd <myprojectdirectory>                     # Move to project directory you want to track
ls -la                                      # List files in directory
git init                                    # Initialize git directory
ls -la                                      # List files in directory -> Note .git folder!
```

What's going on at this point

```bash
git status                                  # Shows what is and is not being tracked
```

What if we have a file(s) that we dont want to track. Use __.gitignore__

```bash
ls -la                                      # List files in directory
touch .gitignore                            # This creates a .gitignore file for us
ls -la                                      # List files in directory -> Note .gitignore file!
```

But how does it know what we want to ignore.
For that, we need to edit the file. Since its just a text file edit any way you wish (e.g. vim, emacs, nano).

```bash
vim .gitignore                              # Use vim to open the file
BoringStuff.xlsx                            # Ignore MS Excel file called BoringStuff
*.txt                                       # Ignore all .txt files
```

Now that we have excluded the junk. Lets tell git to add the rest to the staging area

```bash
git status                                  # Current state of our directory
git add -A                                  # -A add everything (that isn't "gitignored")
git status                                  # Git shows us what changes are ready to be committed
# OR -> add the files individually
git status                                  # Current state of our directory
git add <filename>                          # This will let you to add a file to staging area one at a time
git status                                  # Git shows us what changes are ready to be committed
```

Added file to staging area by accident?

```bash
git status                                  # Current state
git reset BadFile.py                        # Remove BadFile.py from the staging area
git status                                  # Confirm this worked
# OR -> remove all the files and start again
git status                                  # Current state
git reset                                   # Remove all the files from the staging area
git status                                  # Confirm this worked
```

Commit files from the staging area.

```bash
git status                                  # Get a baseline
git commit -m "Initial commit"              # Lets commit, -m is to give it a message, always do this!
git status                                  # Check our staging area
git log                                     # Now we can see our commit along with its message
```

## Remote Repositories

Say we found a project on a remote (e.g., github) that we would like to contribute to.

Copy the remote to local repo.

```bash
git clone <url-source> <local-destination>   # Get url-source from repo repo
#OR
git clone <local-source> <local-destination> # It is rarely needed but you can setup a remote at a different location on your local machine
```

Info about our remote.

```bash
git remote -v                                # Provides information about our remote
git branch -a                                # Shows all branches (local and remote)
```

Making edits to a remote repository.

First, make changes to local repository, and commit.

```bash
git diff                                     # Show changes on current copy of code
git status                                   # Show the files that have been modified
git add -A                                   # Add all the files to staging area
git commit -m "Commit It"                    # Now commit the files on local
```

Second, we pull any new changes that were pushed to the remote while we were working on our local copy, merge our changes, and push the updated files to our remote.

```bash
git pull origin master                       # Now we need to pull, in case someone else has made a change
git push origin master                       # Now we push to origin-name of remote repository and branch - master
```

We have now successfully added our changes to the remote repository!

## Sources

[Git Tutorial from Code Academy](https://www.codecademy.com/learn/learn-git)

[Git Tutorial for Beginners: Command-Line Fundementals](https://www.youtube.com/watch?v=HVsySz-h9r4&t=292s)
