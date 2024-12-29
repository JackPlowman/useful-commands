#  Useful Commands

- [Useful Commands](#useful-commands)
  - [GitHub](#github)
    - [Find all public repositories of a user](#find-all-public-repositories-of-a-user)


## GitHub

### Find all public repositories of a user

This command will list all the public repositories of a user that are not archived and not forked.

```bash
gh repo list --no-archived --source --visibility public --json name --jq '.[].name'
```
