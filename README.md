# Useful Commands

![Maintenance](https://img.shields.io/badge/Maintenance-8A2BE2?style=for-the-badge&color=19e650&label=Status)

## Table of Contents

- [Useful Commands](#useful-commands)
  - [Table of Contents](#table-of-contents)
  - [Git](#git)
    - [Squash all commits of a branch into one](#squash-all-commits-of-a-branch-into-one)
  - [GitHub](#github)
    - [Find all public repositories of a user](#find-all-public-repositories-of-a-user)
  - [Scoop](#scoop)
    - [Update Scoop Packages](#update-scoop-packages)

## Git

### Squash all commits of a branch into one

Reset the branch back to the commit where it was branched from `main` and then commit all the changes in one commit.

```bash
git reset --soft $(git merge-base main HEAD)
git commit -m "Squashed all commits"
```

## GitHub

### Find all public repositories of a user

This command will list all the public repositories of a user that are not archived and not forked.

```bash
# Just the names of the repositories (max 300)
gh repo list --no-archived --source --visibility public -L 300 --json name --jq '.[].name' | sort
```

```bash
# Names of the repositories with the owner (max 300)
gh repo list --no-archived --source --visibility public -L 300 --json nameWithOwner --jq '.[].nameWithOwner' | sort
```

## Scoop

### Update Scoop Packages

```powershell
scoop list | foreach { scoop update $_.Name }
```
