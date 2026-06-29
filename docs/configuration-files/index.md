# Configuration Files

- These files living inside of the `Wokring Directory` instead of living `.git`

## `.gitignore`

- Tells Git which files/folders to ignore (not track)
- Useful for avoiding committing sensitive or temporary files

```cmd
node_modules/
*.log
.env
dist/
```

## `.gitkeep`

- Git doesn't track empty folders, so `.gitkeep` is a convention used to force Git to track them
- You can technically name it anything, like `.keep`, but `.gitkeep` is popular
- With this we can push emptry folders to the remote repository

## `.gitattributes`

- Customize how Git handles certain files — especially line endings, diffing, and merge behaviors.
- You can use it to define custom diff drivers, treat files as binary, or handle language-specific settings

```cmd
*.sh text eol=lf
*.jpg binary
*.md diff=markdown
```

## `.gitmodules`

- Used when your project uses Git submodules

- It lists the repositories and paths for each submodule

```cmd
[submodule "lib/foo"]
    path = lib/foo
    url = https://github.com/example/foo.git
```

## `.gitignore_global`

- Used when you want to globally ignore files (e.g., system files like `.DS_Store`, Thumbs.db)

```cmd
// This should configure globally
git config --global core.excludesfile ~/.gitignore_global
```

## `.gitreview`

- Used in Gerrit code review workflow. Contains review server info.
- Rare unless you're using Gerrit as part of your Git setup.

## `.mailmap`

- Normalize or rewrite author names/emails in logs
- Useful in teams to unify aliases/emails across multiple commits

## Summary

| File               | Purpose                                                           |
|--------------------|-------------------------------------------------------------------|
| `.gitignore`       | Ignore specified files/folders from version control               |
| `.gitkeep`         | Convention to keep empty folders in Git                           |
| `.gitattributes`   | Control file attributes, diff/merge behavior                      |
| `.gitmodules`      | Define Git submodules and their URLs/paths                        |
| `.mailmap`         | Normalize author identity in logs                                 |
| `.gitreview`       | Configure review settings for Gerrit                              |
| `.gitignore_global`| Globally ignored files for all Git projects (configured manually) |
