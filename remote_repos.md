# Remote Repositories

> Joseph P. Vantassel, The University of Texas at Austin

[![License](https://img.shields.io/badge/license-CC--By--SA--4.0-brightgreen.svg)](https://github.com/jpvantassel/git-course/blob/master/LICENSE.md)

## Table of Contents

- [Remote Repository from Local](#Remote-Repository-from-Local)
- [Local Repository from Remote](#Local-Repository-from-Remote)
- [Editing a Remote Repository](#Editing-a-Remote-Repository)

Not what you were looking for? Return to [home](./README.md).

## Remote Repository from Local

First, create a remote repository on [github](https://github.com/).

_Note: If you have not used github before you will need to setup an account._

Second, obtain the remote repository URL.

Third, add remote repository URL to local repository and push commited changes.

```bash
git remote -v                                # Baseline
git remote add origin <remote URL>           # Add remote repo URL
git remote -v                                # View info on remote
git push -u origin master                    # Push commit to master branch.
```

## Local Repository from Remote

```bash
git clone <url-source> <local-destination>   # Clone from URL
#OR
git clone <local-source> <local-destination> # Clone from local machine
```

## Editing a Remote Repository

Make changes to local the repository, commit, pull, and push.

```bash
git diff                                     # Show changes we made
git status                                   # Show modified files
git add -A                                   # Add all modified files to the staging area
git commit -m "Commit It"                    # Commit
git pull                                     # Pull, in case someone else has made a change
git push                                     # Push, our merged changes
```

## Sources

[Git Tutorial from Code Academy](https://www.codecademy.com/learn/learn-git)

[Git Tutorial for Beginners: Command-Line Fundementals](https://www.youtube.com/watch?v=HVsySz-h9r4&t=292s)
