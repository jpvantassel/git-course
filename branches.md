# Git Basics

> Joseph P. Vantassel, The University of Texas at Austin

[![License](https://img.shields.io/badge/license-CC--By--SA--4.0-brightgreen.svg)](https://github.com/jpvantassel/git-course/blob/master/Licence.md)

## Table of Contents

- [Creating a Branch](#Creating-a-Branch)
- [Merging a Branch](#Merging-a-Branch)
  - [Automatic Merge Failed](#Automatic-Merge-Failed)
- [Orphan Branches](#Orphan-Branches)

## Branches

Branches allow us to make speculative changes without affecting our master file.

### Creating a Branch

To create a branch, and begin working.

```bash
git branch                               # List out current branches, and shows current branch by (*)
git branch <branch_name>                 # This creates a new branch
git branch                               # We can now see our new branch
git checkout <branch_name>               # This moves us from our current branch to the branch we just created
git branch                               # Now you can see we are on the new branch
```

We make our speculative changes, and things look good.

First, we need to commit the changes we made to current branch (directions above).

Then push our branch up to our remote.

```bash
git push -u origin <branch_name>         # Now we have associated our local branch and remote branches
git branch -a                            # This will show our local and remote branches
```

### Merging a Branch

If we decide to keep our speculative change, we may want to merge our branch
into master.

```bash
git checkout master                      # Get to our local master branch
git pull origin master                   # Lets pull any new changes
git branch --merged                      # List out the branches we have merged so far
git merge <branch_name>                  # Merge in our branch -> If you get an error see section Automatic Merge Failed
git push origin master                   # Push our changes to master
git branch --merged                      # List out the branches, we should see branch_name here
git branch -d <branch_name>              # Remove the local branch
git branch -a                            # We can see the local branch is gone, but the remote is still there
git push origin --delete <branch_name>   # Now remove the remote branch
git branch -a                            # Now we can see the branches are cleaned up!
```

#### Automatic Merge Failed

If this occurs you will see the message:
`Automatic merge failed; fix conflicts and then commit the result.`. Meaning
that the merge cannot be resolved automatically by git and so requires your
attention. First, see what files are affected with `git status`. Then, starting
at the top of the list, open each file and resolve the conflict.

##### Example

A possible issue may be in your `.gitignore` where you want to ignore a
directory `dist` and `build`. Your master branch has them listed in one order
and your dev branch has them listed in the reverse. When you open your
`.gitignore` you will see something like this.

```bash
<<<<<<< HEAD
dist
build
=======
build
dist
>>>>>>> dev
```

To resolve the conflict decide on which one you want, and delete the other.
If you decided to keep the dev branch version the above snippet would become

```bash
build
dist
```

Save the file. And move onto the next conflict. Once you are done resolving
all the conflicts commit the result as the earlier message instructed.

### Orphan Branches

In certain rare cases, we may want to create an unrelated branch (i.e., an orphan branch)

```bash
git checkout --orphan newbranch          # This moves you to a new empty branch
git log                                  # You will see there are no previous commits
git rm -rf .                             # Remove everything from the current directory and remove from git
# Do some work, so there is something to commit (e.g., touch README.md)
git add -A                               # Add new file(s) to staging area
git commit -m ":tada: Initial Commit"    # Commit new files and establish commit history
git log                                  # Now you can see the history
git branch                               # Now you can see the new orphan branch
git push -u origin <newbranch>           # Now we can push this new orphan branch up to our remote
```

You may wish to track a branch created by one of your collaborators locally.

```bash
git pull                                 # This will notify of 'origin/new_branch'
git branch                               # Note that you still do not have a copy
git checkout --track origin/new_branch   # This will allow you to track it
git branch                               # Can see the branch has been added
```
