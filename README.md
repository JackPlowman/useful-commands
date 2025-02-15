# Useful Commands

- [Useful Commands](#useful-commands)
  - [Git](#git)
    - [Squash all commits of a branch into one](#squash-all-commits-of-a-branch-into-one)
  - [GitHub](#github)
    - [Find all public repositories of a user](#find-all-public-repositories-of-a-user)

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
# Just the names of the repositories
gh repo list --no-archived --source --visibility public --json name --jq '.[].name'
```

```bash
# Names of the repositories with the owner
gh repo list --no-archived --source --visibility public --json nameWithOwner --jq '.[].nameWithOwner'
```
