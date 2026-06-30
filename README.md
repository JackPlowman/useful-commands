# Useful Commands

![Maintenance](https://img.shields.io/badge/Maintenance-8A2BE2?style=for-the-badge&color=19e650&label=Status)

## Table of Contents

- [Useful Commands](#useful-commands)
  - [Table of Contents](#table-of-contents)
  - [Git](#git)
    - [Squash all commits of a branch into one](#squash-all-commits-of-a-branch-into-one)
  - [GitHub](#github)
    - [Find all public repositories of a user](#find-all-public-repositories-of-a-user)
    - [Enable all workflows of all public repositories of a user](#enable-all-workflows-of-all-public-repositories-of-a-user)
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

### Enable all workflows of all public repositories of a user

```bash
USER=your-github-username

export GH_PAGER=cat
export PAGER=cat

gh repo list "$USER" \
  --limit 1000 \
  --visibility public \
  --no-archived \
  --json nameWithOwner,isFork \
  --jq '.[] | select(.isFork == false) | .nameWithOwner' |
while read repo; do
  echo "Checking $repo"

  gh api --paginate "repos/$repo/actions/workflows" \
    --jq '.workflows[] | select(.state != "active") | .id' |
  while read id; do
    echo "  Enabling workflow $id"
    GH_PAGER=cat gh api -X PUT "repos/$repo/actions/workflows/$id/enable"
  done
done
```

## Scoop

### Update Scoop Packages

```powershell
scoop list | foreach { scoop update $_.Name }
```
