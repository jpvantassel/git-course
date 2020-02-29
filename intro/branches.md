# Branches

> Joseph P. Vantassel, The University of Texas at Austin

[![License](https://img.shields.io/badge/license-CC--By--SA--4.0-brightgreen.svg)](https://github.com/jpvantassel/git-course/blob/master/LICENSE.md)

Branches allow us to make speculative changes without affecting our master
branch. This allows us to safely make breaking changes while maintaining a
working copy.

## Creating a Branch

Create local branch.

```bash
git branch                               # List available branches and denotes current branch with *
git branch example                       # Create new branch called example
git branch                               # View our new branch
git checkout example                     # Move from master to the example branch
git branch                               # See that we are on our new branch
```

Make changes to local branch and commit.

```bash
echo "Add some text." > example.txt      # Make a change (e.g., create example file)
git add example.txt                      # Add example file to staging area
git commit -m ":sparkles: Add example"   # Commit file
```

Push our new local branch to remote.

```bash
git branch -a                            # Baseline, note no remote branch
git push -u origin remote_example        # Push new branch to a remote branch remote_example
git branch -a                            # Note newly created remote branch
```

### Renaming a Branch

Rename the branch.

```bash
git branch -m new_name                   # Rename current branch to new_name
# or
git branch -m old_name new_name          # Rename branch old_name to new_name
```

Delete the old remote branch and replace with new branch.

```bash
git push origin :old_name new_name       # Replace remote branch old_name
```

Link newly renamed local and remote branches for future pushes.

```bash
git checkout new_name                    # Switch to newly renamed branch
git push origin -u new_name              # Set branch to update new_name
```

### Create Local Copy of a Remote Branch

If you want to track a remote branch created by a collaborator, you must do so
manually as git does not make local copies of all remote branches by default.

Create local copy of a remote branch.

```bash
git pull                                 # This will notify of 'origin/new_branch'
git branch                               # Note that you do not have a copy
git checkout --track origin/new_branch   # This will allow you to track it
git branch                               # Can see the branch has been added
```

### Create an Orphan Branch

In certain rare cases, we may want to create an unrelated branch
(i.e., an orphan branch).

```bash
git checkout --orphan newbranch          # Move to a new empty branch
git log                                  # Note no previous commits
git rm -rf .                             # Remove everything from the current directory
echo "Do some work" > example.txt        # Do work (e.g., create new file)
git add -A                               # Add new file(s) to staging area
git commit -m ":tada: Initial Commit"    # Commit new files and establish history
git log                                  # View history
git branch                               # View new orphan branch
git push -u origin newbranch             # Push orphan branch to remote
```

## Merging a Branch

If we decide we like our speculative changes we can merge it into our master
branch.

Merge branch into master.

```bash
git checkout master                      # Move to master branch
git pull origin master                   # Pull any new changes
git branch --merged                      # List out the branches we have merged to date
git merge example                        # Merge in our branch -> If you get an error see section Automatic Merge Failed
git push origin master                   # Push our changes to master
git branch --merged                      # Note new newly merged branch has been added
```

### Automatic Merge Failed

A common error when merging branches is
`Automatic merge failed; fix conflicts and then commit the result.`. This error
indicates that merge could not be resolved automatically by git and so requires your
attention.

To resolve the failed merge

1. `git status` - To view what files were affected.
2. Starting at the top move systematically through the list resolving conflicts (see [example](#Example))
3. Commit the result of your manual merge.

#### Example

A possible issue may be in your `.gitignore` where you want to ignore a
directory `dist` and `build`. Your master branch has them listed in one order
and your dev branch has them listed in the reverse. When you open your
`.gitignore` you will see.

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
all the conflicts commit the result.

## Deleting a Branch

After we merge our branch into master, we may wish to delete it.

Delete local branch.

```bash
git branch -a                            # After merging branch still exists
git branch -d example                    # Remove the local branch example
git branch -a                            # Local branch is gone, but the remote is still there
```

Delete remote branch.

```bash
git branch -a                            # After deleting local branch remote still exists
git push origin --delete example         # Remove remote branch
git branch -a                            # All done!
```

## Sources

[Git Tutorial from Code Academy](https://www.codecademy.com/learn/learn-git)

[Git Tutorial for Beginners: Command-Line Fundementals](https://www.youtube.com/watch?v=HVsySz-h9r4&t=292s)

[Rename a Local and Remote Branch](https://multiplestates.wordpress.com/2015/02/05/rename-a-local-and-remote-branch-in-git/)
