# Commits

## Commit Types

| Type        | Purpose                                      |
|-------------|----------------------------------------------|
| `feat`      | A new feature                                |
| `fix`       | A bug fix                                    |
| `docs`      | Documentation only changes                   |
| `style`     | Formatting (no code change)                  |
| `refactor`  | Code change that is not a fix or feature     |
| `test`      | Adding or fixing tests                       |
| `chore`     | Maintenance tasks like config updates        |

## Write a Perfect Commit

- Structure of a perfect commit

```cmd
<type>(optional scope): <short summary>

<detailed description / body>

<footer (optional)>
```

- Manually in the terminal

```cmd
git commit
```

```cmd
feat(auth): add JWT login support

This implements secure user authentication using JSON Web Tokens.
It includes middleware for token validation and user role checking.

Closes #42
```

- Inline in the terminal (only for short ones) / (Each `-m` means new line / paragraph)

```cmd
git commit -m "feat(auth): add JWT login support" -m "Implements login with token authentication and user role handling." -m "Closes #42"
```
