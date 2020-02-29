# Tags

> Joseph P. Vantassel, The University of Texas at Austin

[![License](https://img.shields.io/badge/license-CC--By--SA--4.0-brightgreen.svg)](https://github.com/jpvantassel/git-course/blob/master/Licence.md)

## Introduction

Git offers two types of tags, _Lightweight_ and _Annotated_.

- _Lightweight:_ tags are the simplest and mark the commit with only the tag name.
- _Annotated:_ tags mark the commit and other additional information such as tagger, tag date, and tag message.

## Creating Lightweight Tags

```bash
git tag -l                               # List out current tags
git tag v0.1.0                           # Create lightweight local tag
git tag -l                               # List out current tags -> note v0.1.0
git tag v0.1.0                           # View newly created tag specifically
git push origin --tags                   # Push the tag up to the remote
```

## Creating Annotated Tags

```bash
git tag -l                               # List out current tags
git tag -a v0.1.1 -m "Release v0.1.0"    # Create annotated tag
git tag -l                               # List out current tags -> note v0.1.1
git tag v0.1.1                           # View new tag. Note additional info.
git push origin --tags                   # Push the tag up to the remote
```

## Deleting a Tag

If you accidentally created a tag, you can delete it by.

```bash
git tag -l                               # List out current tags
git tag -d <spec-tag>                    # delete tag
git tag -l                               # Note tag is gone
git push origin --delete <spec-tag>      # Remove that tag from our remote
```

## Forgot to Add a Tag

If you forgot to add a tag in the past and would like to add it retroactively.

```bash
git tag -l                               # List out current tags
git tag -a v0.2.1 -m "tag-msg" hash      # Create annotated tag, for an old commit
git tag -l                               # List out current tags -> note v0.1.1
git push origin --tags                   # Push the tag up to the remote
```

## Sources

[Git - Tagging](https://git-scm.com/book/en/v2/Git-Basics-Tagging)
