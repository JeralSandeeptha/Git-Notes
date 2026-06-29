# Mistakes

| Task                             | Command                          |
|----------------------------------|----------------------------------|
| Unstage file                     | `git reset <file>`               |
| Undo last commit (keep changes)  | `git reset --soft HEAD~1`        |
| Revert a commit                  | `git revert <commit>`            |
| Restore the file changes         | `git restore <>file`             |

## Reset

```cmd
git reset [<mode>] [<commit>]
```

- Modes

| Mode      | Affects                    | Description                                           |
| --------- | -------------------------- | ----------------------------------------------------- |
| `--soft`  | HEAD only                  | Move HEAD to a previous commit, keep changes staged   |
| `--mixed` | HEAD + index               | Default mode. Unstage changes, keep working directory |
| `--hard`  | HEAD + index + working dir | Discard all changes completely                        |

```cmd
git reset --soft HEAD~1
git reset --mixed HEAD~1
git reset --hard HEAD~1
git reset <file>
git reset --hard <commit-hash>
```

- Summary

| Command                     | Effect                                        |
| --------------------------- | --------------------------------------------- |
| `git reset --soft HEAD~1`   | Undo last commit, keep changes staged         |
| `git reset --mixed HEAD~1`  | Undo last commit, unstage changes             |
| `git reset --hard HEAD~1`   | Undo last commit, delete changes              |
| `git reset <file>`          | Unstage a file (preserve changes)             |
| `git reset --hard <commit>` | Reset to commit and erase everything after it |
