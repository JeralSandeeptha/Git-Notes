# Commands

## 🔍 Check Git Version

- Displays the installed Git version

```cmd
git version
```

## ⚙️ Configure user

```cmd
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

## ⚙️ View Git Configuration

- Lists all Git configuration settings (user name, email, editor, etc.)

```cmd
git config -l
```

## 🧱 Initialize a Git Repository

- Creates a new Git repository in the current directory by adding a .git/ folder

```cmd
git init
```

## 📂 Check Current Status

- Shows the status of files in the working directory and staging area

```cmd
git status
```

## ➕ Stage Files

- Stages modified and untracked files

```cmd
git add .
git add index.html
```

## ❌ Unstage a File

- Remove files from stage

```cmd
git rm --cached index.html
```

## 📝 Commit Changes

- Creates a new commit with a message

```cmd
git commit -m "added"
```

## 📜 View Commit History

- See commit history

```cmd
git log

git log --oneline
```

## 🔍 Show Specific Commit

- Inspect the commits

```cmd
git show <commit-hash>
```

## 🌱 Create a New Branch

- Create local branch

```cmd
git branch feature-1
```

## 🌿 Switch Branches

```cmd
git checkout feature-1

git checkout -b feature-1
```

## 🧹 Delete Branches

- Delete local branch

```cmd
git branch -d feature-1
```

- Delete remote branch

```cmd
git push origin --delete feature-1
```

## 🌿 List Local and Remote Branches

- Local Branches

```cmd
git branch
```

- Remote Branches

```cmd
git branch -r
```

## ⬆️ Push Changes to Remote Repository

- Push chnages to remote branch

```cmd
git push

git push origin main

git push -u origin main
```

## ⬇️ Pull Changes from Remote

- Get latest code from remote branch

```cmd
git pull origin dev
```

## 🔀 Merge Branches

- To merge branches

```cmd
git merge feature-1
```

## 🌍 Remote Collaboration

- Add remote repository

```cmd
git remote add origin https://github.com/user/repo.git
```

## 🔍 Get Remote Branches

- Get all the remote repository branches into local repository

```cmd
git fetch
```

## ⬇️ Clone Project

- Clone remote repository

```cmd
git clone https://github.com/user/repo.git
```

---

## Summary

| Task                        | Command                         |
|-----------------------------|---------------------------------|
| Initialize Git in a project | `git init`                      |
| Clone a remote repo         | `git clone <url>`               |
| Check status                | `git status`                    |
| Add file(s) to staging      | `git add <file>` or `git add .` |
| Commit staged files         | `git commit -m "Message"`       |
| View commit history         | `git log`                       |
| Show changes                | `git diff`                      |
| Create a branch             | `git branch <name>`             |
| Switch branch               | `git checkout <name>`           |
| Create + switch             | `git checkout -b <name>`        |
| Merge branch                | `git merge <branch>`            |
| Push changes                | `git push origin <branch>`      |
| Pull changes                | `git pull`                      |
| Add a remote                | `git remote add origin <url>`   |
