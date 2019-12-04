# Git Basics

> Joseph P. Vantassel, The University of Texas at Austin

[![License](https://img.shields.io/badge/license-CC--By--SA--4.0-brightgreen.svg)](https://github.com/jpvantassel/git-course/blob/master/Licence.md)

## Fixing Common Mistakes

### Fixes that do not effect the history

Go back to previous commit.

```bash
git status                       # Can see the files have changed
git diff                         # Can see the changes
git checkout <filename>          # Lets reset our file to last commit
git status                       # Can see file has been rolled back
git diff                         # Can see there are no changes in file
```

If collaborator has already pulled the file.

```bash
git log                          # See our commits, get hash
git revert hash                  # Allows us to revert,
git log                          # Now can see an additional commit undoing changes
git diff hash1 hash2             # Let us see what git did to maintain history.
```

### Fixes that do affect the history

Bad commit message.

```bash
git log                         # Current log
git commit --amend -m "My Msg"  # Change commit message
git log                         # New log, see changed message, but new hash!
```

Forgot to include file.

```bash
git add <forgotten file>        # Place forgotten file in staging file
git commit --amend              # Going to amend
git log                         # See no new commit
git log --stat                  # See files that were changed in commit
```

Making changes on master rather than feature branch

```bash
git log                         # Lets get the hash of the commit we want to copy
git checkout branch_name        # Go to the branch we were supposed to have committed to
git log                         # Can see we don't have the commit
git cherry-pick hashmaster      # Brings commit onto feature branch
git log                         # See the copied commit

#Now we need to remove the bad commit from master

git checkout master             # Go back to the master branch
git log                         # Get hash of the commit we want
git reset --soft hash           # Commit is gone, files still has changed and are in staging area
git reset hash                  # Mixed (default). Commit gone, files still have changes, but are not in staging area
git reset --hard hash           # Commit gone, tracked files set back to commit
git clean -df                   # This cleans out all untracked (d for directories, f for files)
```

Ran ```git reset --hard``` by accident. There may be hope if its <30 days.

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

If you accidentally committed a large file to your git history, but are now
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

Note that if you add this file to .gitignore and try committing this will not
solve your problem as the issue is with your very first commit (the one before
you realized you have that large file).

To fix this issue you need to not only .gitignore the large file, but also purge
this file from your commit history so you can push your work and be up to update
on your remote. You do this by going back in your tree and forcefully removing
the file.

```bash
git filter-branch --tree-filter 'rm -rf path/to/your/large/file' HEAD
```

If you need to do this for more than one file, you will need to add a -f, to
tell github to force overwrite the backup it made when you performed the previous
filter and removal, like this:

```bash
git filter-branch -f --tree-filter 'rm -rf path/to/your/other/large/file' HEAD
```

## Renaming a GitHub Repository

On github

```bash
Your Repo > Settings > Repository name
```

Links to the previous name of your repository will be forwarded to your new
repository. However, for clarity its recommend that you update your links by:

```bash
git remote set-url origin <newurl>
```

## Sources

[Git Tutorial: Fixing Common Mistakes and Undoing Bad Commits](https://www.youtube.com/watch?v=FdZecVxzJbk&t=56s)

[Committed a Large File by Accident?](https://thomas-cokelaer.info/blog/2018/02/git-how-to-remove-a-big-file-wrongly-committed/)
