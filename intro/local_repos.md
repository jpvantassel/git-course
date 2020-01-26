# Local Repositories

> Joseph P. Vantassel, The University of Texas at Austin

[![License](https://img.shields.io/badge/license-CC--By--SA--4.0-brightgreen.svg)](https://github.com/jpvantassel/git-course/blob/master/LICENSE.md)

## Create a Local Repository

```bash
cd <myprojectdirectory>                # Move to project directory you want to track
ls -la                                 # List all files, one per line in directory
git init                               # Initialize git directory
ls -la                                 # Note newly created .git directory!
echo "Hello" > example.txt             # Create example file so directory is not empty
git status                             # Shows what is and is not being tracked
```

## Ignoring files

To ignore a file add its name to a `.gitignore` file.

```bash
git status                             # Shows state of the repo, note example.txt is not tracked
ls -la                                 # List files in directory
echo "example.txt" > .gitignore        # This creates a .gitignore file for us
ls -la                                 # List files in directory -> Note .gitignore file!
git status                             # Note that example.txt no longer appears
```

_Note: You can use wildcard expansion in your `.gitignore` to ignore types of
files in your repository. For example `*.txt` would ignore all files with a
`.txt` extension._

## Add File(s) to the Staging Area

```bash
git status                             # Current state of our directory
git add <filename>                     # Add a single file to the staging area
# OR -> To add all
git add -A                             # Add everything that isn't "ignored"
git status                             # Git shows us what changes are ready to be committed
```

## Remove File(s) from the Staging Area

```bash
git status                             # Baseline
git reset BadFile.py                   # Remove BadFile.py from the staging area
# OR -> To remove all
git reset                              # Remove all staged files from the staging area
git status                             # Confirm this worked
```

### Commit Staged File

```bash
git status                             # Baseline
git commit -m ":tada: Initial commit"  # Commit, -m is to give it a message, always do this!
git status                             # Check our staging area
git log                                # Now we can see our commit along with its message
```

_Note: The `:tada:` in the above commit message will render as an emoji on
github. Developers use commit emojis to communicate what the commit was about,
without using text. A listing of the commit emojis that I use in my projects is
provided [here](./emojis.md)._

## Sources

[Git Tutorial from Code Academy](https://www.codecademy.com/learn/learn-git)

[Git Tutorial for Beginners: Command-Line Fundementals](https://www.youtube.com/watch?v=HVsySz-h9r4&t=292s)
