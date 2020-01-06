# Fixing Common Mistakes

> Joseph P. Vantassel, The University of Texas at Austin

[![License](https://img.shields.io/badge/license-CC--By--SA--4.0-brightgreen.svg)](https://github.com/jpvantassel/git-course/blob/master/LICENSE.md)

## Table of Contents

- [Fixes that do not affect history](#Fixes-that-do-not-affect-the-history)
  - [Return to last commit](#Return-to-Last-Commit)
- [Fixes that do affect history](#Fixes-that-do-affect-the-history)
  - [Amend Bad Commit Message](#Amend-Bad-Commit-Message)
  - [Forgot to Include File](#Forgot-to-Include-File)
  - [Made Changes on Master by Mistake](#Made-Changes-On-Master-By-Mistake)
  - [Accidental Hard Reset](#Accidental-Hard-Reset)
- [Commited a Large File by Accident](#Commited-a-Large-File-by-Accident)
- [Renaming a Remote Repository](#Renaming-a-Remote-Repository)

Not what you were looking for? Return to [home](./README.md).

## Fixes that do not affect the history

### Return to Last Commit

```bash
git status                       # Can see the files have changed
git diff                         # Can see the changes
git checkout <filename>          # Reset file to last commit
git status                       # Can see file has been rolled back
git diff                         # Can see there are no changes in file
```

<!-- If collaborator has already pulled the file.
TODO (jpv) Understand what is going on here.
```bash
git log                          # See our commits, get hash
git revert hash                  # Allows us to revert to specific hash
git log                          # Now can see an additional commit undoing changes
git diff hash1 hash2             # See what git did to maintain history.
``` -->

## Fixes that do affect the history

### Amend Bad Commit Message

```bash
git log                         # Current log
git commit --amend -m "My Msg"  # Change commit message
git log                         # New log, see changed message, but new hash!
```

### Forgot to Include File

```bash
git add <forgotten file>        # Place forgotten file in staging file
git commit --amend              # Going to amend
git log                         # See no new commit
git log --stat                  # See files that were changed in commit
```

### Made Changes on Master By Mistake

```bash
git log                         # Lets get the hash of the commit we want to copy
git checkout branch_name        # Go to the branch we were supposed to have committed to
git log                         # Can see we don't have the commit
git cherry-pick hashmaster      # Brings commit onto feature branch
git log                         # See the copied commit

git checkout master             # Go back to the master branch
git log                         # Get hash of the commit we want
git reset --soft hash           # Commit is gone, files still has changed and are in staging area
git reset hash                  # Mixed (default). Commit gone, files still have changes, but are not in staging area
git reset --hard hash           # Commit gone, tracked files set back to commit
git clean -df                   # This cleans out all untracked (d for directories, f for files)
```

### Accidental Hard Reset

There is some hope for this to be sucessful if the hard reset was done no
longer than 30 days ago.

```bash
git reflog                      # This keeps track of all changes, might see hash
git checkout hash               # This brings you back, but in a "detached head state" (i.e. not on a branch)
git log                         # Can now see the changes are back
git branch branchname           # Add a branch to save that work, if we dont it will get deleted
git branch                      # We can see our current branch and new branch
git checkout master             # Go to master
git branch                      # See all our branches, note that "detached head state" branch is gone
```

## Commited a Large File by Accident

You accidentally commited a large file to your local repo but are now
having an issue pushing your commit due to Github's maximum file size of 100MB.

When you push you will see an error like this:

```bash
remote: error: GH001: Large files detected. You may want to try Git Large File Storage - https://git-lfs.github.com.
remote: error: Trace: b310dac0473fe3f34910f9b68bd885fd
remote: error: See http://git.io/iEPt8g for more information.
remote: error: File path/to/your/file is 427.54 MB; this exceeds GitHubs file size limit of 100.00 MB
To github.com:username/repository.git
 ! [remote rejected] master -> master (pre-receive hook declined)
error: failed to push some refs to git@github.com:username/repository.git
```

_Note: If you add this file to the repositories `.gitignore` and try committing
again this will not solve your problem as the issue is with your first
commit (the one before you realized you have that large file)._

To fix this issue you need to not only `.gitignore` the large file, but also
purge this file from your commit history so you can push your work and be up to
update on your remote. You do this by going back in your tree and forcefully
removing the file.

```bash
git filter-branch --tree-filter 'rm -rf path/to/your/large/file' HEAD
```

If you need to do this for more than one file, you will need to add a `-f`, to
tell github to force overwrite the backup it made when you performed the
previous filter and removal, like this.

```bash
git filter-branch -f --tree-filter 'rm -rf path/to/your/other/large/file' HEAD
```

## Renaming a Remote Repository

On github

```bash
Your Repo > Settings > Repository name
```

Links to the previous name of your repository will be forwarded to your new
repository. However, for clarity its recommend that you update your links.

```bash
git remote set-url origin <newurl>
```

## Sources

[Git Tutorial: Fixing Common Mistakes and Undoing Bad Commits](https://www.youtube.com/watch?v=FdZecVxzJbk&t=56s)

[Committed a Large File by Accident?](https://thomas-cokelaer.info/blog/2018/02/git-how-to-remove-a-big-file-wrongly-committed/)
