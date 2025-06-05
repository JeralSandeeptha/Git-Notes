# GIT Version Control

## Table of Contents
- [Introduction](#introduction)
- [How GIT Works](#how-git-works)
- [Configuration Files](#configuration-files)
- [Core Concepts](#core-concepts)
- [Git Workflow](#git-workflow)
- [Commands](#commands) 
- [Best Pratices](#best-pratices)
- [Mistakes](#mistakes)
- [Commits](#commits)
- [Merging](#merging)
- [Resolve Merge Conflicts](#resolve-merge-conflicts)
- [Branching Stratergies](#branching-stratergies)

<br /><br />

## Introduction
- `GIT` is a memory card for codebase
- `GIT` is a content tracker. We can track any content
- `GIT` is a distributed version control system (VCS) that helps developers track changes to files (usually code), collaborate with others, and manage different versions of a project

- [Watch this tutorial playlist](https://www.youtube.com/watch?v=fWMKue-WBok&list=PL9lx0DXCC4BNUby5H58y6s2TQVLadV8v7)

<br /><br />

## How GIT Works

![GIT simple diagram](https://res.cloudinary.com/djgwvmcdl/image/upload/v1748952000/6194709048910268702_lz8krp.jpg)

[Refer GIT Workflow Behind the Scenes](https://octobot.medium.com/how-git-internally-works-1f0932067bee)

#### GIT Objects

![Image](https://res.cloudinary.com/djgwvmcdl/image/upload/v1748953268/6194709048910268730_weoeek.jpg)
![Image](https://res.cloudinary.com/djgwvmcdl/image/upload/v1748953702/6194709048910268731_ttj6ch.jpg)
![Image](https://res.cloudinary.com/djgwvmcdl/image/upload/v1748953801/6194709048910268732_bf1rg8.jpg)
![Image](https://res.cloudinary.com/djgwvmcdl/image/upload/v1748953854/6194709048910268733_ro07q5.jpg)
![Image](https://res.cloudinary.com/djgwvmcdl/image/upload/v1748953915/6194709048910268734_r4qfc5.jpg)

![Relation between Objects](https://res.cloudinary.com/djgwvmcdl/image/upload/v1748897883/d97d7063-81af-44d9-8038-0b8bbaae4d1d_m9o1ld.jpg)

- We can use this commands to identify the obejcts and it contents
![Image](https://res.cloudinary.com/djgwvmcdl/image/upload/v1748982100/1_keKQzsPTjdTJJm81xEqO1A_epean2.webp)

- Everything is stored as objects in a `.git/objects` directory
- `.git/objects` directory is like a database of `git`
- `Git` has 4 fundamental object types

![Objects](https://res.cloudinary.com/djgwvmcdl/image/upload/v1748897995/fYm0s_i6veqf.png)
[Indeep Knowledege about Objects](https://medium.com/mindorks/what-is-git-object-model-6009c271ca66)

- For a git project we need atleast `object store` and `reference store`
- They are represents `objects` and `refs` folders
![Image](https://res.cloudinary.com/djgwvmcdl/image/upload/v1748980250/gitdatabase3_xtrivt.webp)

| Object Type | Description                                          |
|-------------|------------------------------------------------------|
| **Blob**    | Stores file content                                  |
| **Tree**    | Stores directory structure (list of blobs and trees) |
| **Commit**  | Points to a tree and holds commit metadata           |
| **Tag**     | Used to tag commits (like releases)                  |

##### 📦 1. Blob (Binary Large Object)
- Stores file contents (just the content, no filename or metadata)
- Git creates a blob for each file when added
- If you add a file `hello.txt` with content Hello, Git stores a `blob` object with that content

##### 🌲 2. Tree
- Represents a `directory`
- Holds references to `blobs` (files) and other `trees` (subdirectories)
- Stores file names and permissions
```cmd
tree
├── file1.txt (blob)
├── dir/ (tree)
│   └── file2.txt (blob)
```

##### 📝 3. Commit
- Points to a `tree` (the root directory of that commit)
- Contains metadata
```cmd
Commit Object:
tree <tree_hash>
parent <parent_hash>
author You <email@example.com>
committer You <email@example.com>

Commit message
```

##### 🔖 4. Tag
- Tags point to a commit.
- Can be lightweight or annotated.
- Annotated tags are stored as objects and include tagger name, date, and message.
```cmd
git tag v1.0
```

##### 🧠 How Git stores them
- Every Git object is stored in .git/objects by splitting the hash:
```git
.git/objects/ab/cdef1234...   ← where `ab` is the first 2 chars of the hash
```

#### Folder Structure
- This is the folder structure of `.git` folder
```cmd
.git/
├── HEAD
├── config
├── description
├── hooks/
├── info/
├── objects/
├── refs/
├── index
└── logs/
```

#### 📂 Important Directories  
##### 🔧 `hooks/`
- Contains **sample Git hooks** (e.g., `pre-commit.sample`, `post-merge.sample`).
- Hooks are shell scripts that run automatically on specific Git events.
- You can create **custom automation** like:
  - Linting code before commits
  - Preventing pushes to `main`
  - Sending notifications on merge

> 🧪 Example: Rename `pre-commit.sample` to `pre-commit` and make it executable.

##### ℹ️ `info/`
- Contains the `exclude` file.
- Works like `.gitignore`, but it is **local-only** (not tracked by Git).
- Useful for ignoring personal or temporary files **without modifying `.gitignore`**.

##### 🧱 `objects/`
- This is the **Git database**.
- Stores all content (commits, trees, blobs) as **hashed objects**.
- Structure:

##### 🔗 `refs/`
- Stores **pointers to commits**.
- Subfolders:
- `refs/heads/` → Local branches
- `refs/tags/` → Tags
- `refs/remotes/` → Remote tracking branches (e.g., `origin/main`)

##### 🧾 `logs/`
- Contains **logs of reference updates**.
- Tracks movements of `HEAD`, branches, etc.
- Example: `logs/HEAD`, `logs/refs/heads/main`
- Extremely useful for:
- Recovering lost commits
- Understanding branch movement history

> 🛠 Use `git reflog` to see these logs.

<br />

#### ✅ Key Files in `.git`
- These are the key files which is generated by default

| File / Folder   | Purpose                                                                 |
|------------------|-------------------------------------------------------------------------|
| `HEAD`           | Points to the current branch or commit. Usually contains `ref: refs/heads/main`. |
| `config`         | Repository-specific configuration (like remotes, user name/email, etc.). |
| `description`    | Used by Gitweb (web interface) for describing the repo.                |
| `index`          | Staging area (also called the cache); tracks what is currently staged. |
| `packed-refs`    | Stores packed references (e.g., branch heads, tags) to save space.     |


#### 🧪 Optional / Generated Files
- These file are generating while some specific operations

| File/Directory           | Purpose                                                                 |
|--------------------------|-------------------------------------------------------------------------|
| `MERGE_HEAD`             | Exists during a merge conflict to indicate the other commit being merged. |
| `ORIG_HEAD`              | Stores the previous HEAD (useful for undoing operations like reset).    |
| `COMMIT_EDITMSG`         | Message from the last commit, used by Git when creating a commit.       |
| `FETCH_HEAD`             | Created during `git fetch` to record what was fetched.                  |
| `rebase-apply/` or `rebase-merge/` | Temporary directories used during rebasing.                         |

## Configuration Files
- These files living inside of the `Wokring Directory` instead of living `.git`

#### `.gitignore`
- Tells Git which files/folders to ignore (not track)
- Useful for avoiding committing sensitive or temporary files
```cmd
node_modules/
*.log
.env
dist/
```

#### `.gitkeep`
- Git doesn't track empty folders, so `.gitkeep` is a convention used to force Git to track them
- You can technically name it anything, like `.keep`, but `.gitkeep` is popular
- With this we can push emptry folders to the remote repository 

#### `.gitattributes`
- Customize how Git handles certain files — especially line endings, diffing, and merge behaviors.
- You can use it to define custom diff drivers, treat files as binary, or handle language-specific settings.
```cmd
*.sh text eol=lf
*.jpg binary
*.md diff=markdown
```

#### `.gitmodules`
- Used when your project uses Git submodules.
- It lists the repositories and paths for each submodule.
```cmd
[submodule "lib/foo"]
    path = lib/foo
    url = https://github.com/example/foo.git
```

#### `.gitignore_global`
- Used when you want to globally ignore files (e.g., system files like `.DS_Store`, Thumbs.db).
```cmd
// This should configure globally
git config --global core.excludesfile ~/.gitignore_global
```

#### `.gitreview`
- Used in Gerrit code review workflow. Contains review server info.
- Rare unless you're using Gerrit as part of your Git setup.

#### `.mailmap`
- Normalize or rewrite author names/emails in logs
- Useful in teams to unify aliases/emails across multiple commits

#### Summary
| File               | Purpose                                                        |
|--------------------|----------------------------------------------------------------|
| `.gitignore`       | Ignore specified files/folders from version control            |
| `.gitkeep`         | Convention to keep empty folders in Git                        |
| `.gitattributes`   | Control file attributes, diff/merge behavior                   |
| `.gitmodules`      | Define Git submodules and their URLs/paths                     |
| `.mailmap`         | Normalize author identity in logs                              |
| `.gitreview`       | Configure review settings for Gerrit                           |
| `.gitignore_global`| Globally ignored files for all Git projects (configured manually) |

<br /><br />

## Core Concepts
| Term                     | Meaning                                                          |
| ------------------------ | ---------------------------------------------------------------- |
| **Repository (repo)**    | A Git-managed project (a `.git` folder exists in it)             |
| **Working directory**    | Your project folder with code                                    |
| **Staging area (index)** | A place to prepare files before committing                       |
| **Commit**               | A saved snapshot of your project                                 |
| **Branch**               | A pointer to a series of commits                                 |
| **Merge**                | Combine changes from different branches                          |
| **Remote**               | A shared version of your repository hosted online (e.g., GitHub) |
| **Clone**                | Copy a remote repo to your computer                              |

<br /><br />

## Git Workflow
- ![Git Workflow Basic 1](https://res.cloudinary.com/djgwvmcdl/image/upload/v1748881639/GitWorkflow-3_u0cxta.png)
- ![Git Workflow Basic 2](https://res.cloudinary.com/djgwvmcdl/image/upload/v1748881649/1_W1LPtxxrJ0J1cq_Pv_OWbQ_xkg9kp.png)
- ![Git Workflow Advance](https://res.cloudinary.com/djgwvmcdl/image/upload/v1748881657/git_icon-781e4cc0_gdwiuw.png)
- ![Git Branching](https://res.cloudinary.com/djgwvmcdl/image/upload/v1748881897/1_S4VJPf8Mrg3Gn5cR7JK62w_czyxzp.png)

<br /><br />

## Commands

#### 🔍 Check Git Version
- Displays the installed Git version
```cmd
git version
```

#### ⚙️ Configure user
```cmd
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

#### ⚙️ View Git Configuration
- Lists all Git configuration settings (user name, email, editor, etc.)
```cmd
git config -l
```

#### 🧱 Initialize a Git Repository
- Creates a new Git repository in the current directory by adding a .git/ folder
```cmd
git init
```

#### 📂 Check Current Status
- Shows the status of files in the working directory and staging area
```cmd
git status
```

#### ➕ Stage Files
- Stages modified and untracked files
```cmd
git add .
git add index.html
```

#### ❌ Unstage a File
- Remove files from stage
```cmd
git rm --cached index.html
```

#### 📝 Commit Changes
- Creates a new commit with a message
```cmd
git commit -m "added"
```

#### 📜 View Commit History
- See commit history
```cmd
git log

git log --oneline
```

#### 🔍 Show Specific Commit
- Inspect the commits
```cmd
git show <commit-hash>
```

#### 🌱 Create a New Branch
- Create local branch
```cmd
git branch feature-1
```

#### 🌿 Switch Branches
```cmd
git checkout feature-1

git checkout -b feature-1
```

#### 🧹 Delete Branches
- Delete local branch
```cmd
git branch -d feature-1
```
- Delete remote branch
```cmd
git push origin --delete feature-1
```

#### 🌿 List Local and Remote Branches
- Local Branches
```cmd
git branch
```
- Remote Branches
```cmd
git branch -r
```

#### ⬆️ Push Changes to Remote Repository
- Push chnages to remote branch
```cmd
git push

git push origin main

git push -u origin main
```

#### ⬇️ Pull Changes from Remote
- Get latest code from remote branch
```cmd
git pull origin dev
```

#### 🔀 Merge Branches
- To merge branches
```cmd
git merge feature-1
```

#### 🌍 Remote Collaboration
- Add remote repository
```cmd
git remote add origin https://github.com/user/repo.git
```

#### 🔍 Get Remote Branches
- Get all the remote repository branches into local repository
```cmd
git fetch
```

#### ⬇️ Clone Project
- Clone remote repository
```cmd
git clone https://github.com/user/repo.git
```

#### Summary
| Task                        | Command                         |
|-----------------------------|----------------------------------|
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

<br /><br />

## Best Pratices
- Use `.gitignore` to exclude unwanted files
- Write clear commit messages
- Create separate branches for features/bugs
- Pull before you push
- Use `git log --oneline` to view history concisely

<br /><br />

## Mistakes
| Task                            | Command                          |
|----------------------------------|----------------------------------|
| Unstage file                    | `git reset <file>`              |
| Undo last commit (keep changes) | `git reset --soft HEAD~1`       |
| Revert a commit                 | `git revert <commit>`           |
| Restore the file changes               | `git restore <>file`           |

#### Reset
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

<br /><br />

## Commits

#### Commit Types
| Type     | Purpose                                      |
|----------|----------------------------------------------|
| `feat`   | A new feature                                |
| `fix`    | A bug fix                                    |
| `docs`   | Documentation only changes                   |
| `style`  | Formatting (no code change)                  |
| `refactor` | Code change that is not a fix or feature   |
| `test`   | Adding or fixing tests                       |
| `chore`  | Maintenance tasks like config updates        |

#### Write a Perfect Commit

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

<br /><br />

## Merging
- `Merging` in Git is the process of combining changes from one branch into another — most commonly, from a `feature branch` into `main` / `child branch` into `parent branch`.

```cmd
# Step 1: Switch to the branch you want to merge into (usually main)
git checkout main

# Step 2: Merge the other branch into this one
git merge feature-x
```

- There are several ways to merge branches
    - `Merge`
    - `Rebase`

- `Merge` option, it also requires a commit to it's parent for merge. If there are many commits those commits combine into single commit and merge as a single commit.
![Merge](https://res.cloudinary.com/djgwvmcdl/image/upload/v1748893501/492bbdd4d1c256ad4b07c9a042fd18fca353b1cc_eb1o91.png)

- `Rebase` option, replays changes from one line of work onto another in the order they were introduced, whereas merging takes the endpoints and merges them together.
![Rebase](https://res.cloudinary.com/djgwvmcdl/image/upload/v1748893771/1_mQOZjM3wwL1UV-ydQYAJTg_ieqpln.webp)

<br /><br />

## Resolve Merge Conflicts
- A `Merge Conflict` in Git occurs when the automatic merging of two branches fails because there are conflicting changes to the same file or lines of code. This happens when different developers have made changes to the same section of a file in separate branches.

![Merge Conflict 1](https://res.cloudinary.com/djgwvmcdl/image/upload/v1748892660/conflict_lpxncs.png)
![Merge Conflict 2](https://res.cloudinary.com/djgwvmcdl/image/upload/v1748892693/_cover.qr_5Xx8L_20OKOC_ijekgz.webp)

- We can do 3 things when a merge conflict
    - Accept current changes
    - Accept incoming changes
    - Accept both changes

- Merge Conflict Resolve Process
    - Pull the new code
    - Remove the markers
    - Keep whatever you want
    - Save, Stage and Commit the new changes

<br /><br />

## Branching Stratergies
- Branching Strategy depends on team's `workflow`, `project type`, `deployment process`.

- Team size: 
    - Smaller teams might prefer `GitHub Flow` or `Trunk-Based Development`, while larger teams may opt for `Git Flow`.

- Deployment frequency: 
    - Continuous deployment favors lightweight strategies like `GitHub Flow`.

- Project complexity: 
    - Complex projects with long-lived features benefit from `Git Flow` or `Release Branching`.

### Git Flow

![Git Flow Diagram](https://wac-cdn.atlassian.com/dam/jcr:cc0b526e-adb7-4d45-874e-9bcea9898b4a/04%20Hotfix%20branches.svg?cdnVersion=2757)

#### Description
A robust strategy with dedicated branches for feature development, releases, and hotfixes.

#### Branches

- **main / master** – Latest production-ready code.
- **develop/** – Integrates new features for the next release.
- **feature/** – For individual features.
- **release/** – For stabilising code before a production release.
- **hotfix/** – For quick fixes on the production code.

#### Usage
Suitable for large projects with scheduled releases.

### GitHub Flow

![GitHub Flow Diagram](https://res.cloudinary.com/djgwvmcdl/image/upload/v1748952160/6194709048910268704_sht6gj.jpg)

#### Description
A simplified, lightweight strategy for continuous delivery.

#### Branches

- **main / master** – Latest production-ready code.
- **feature/** – Short-lived branches for new features or bug fixes.

#### Workflow

1. Create a feature branch from `main`.
2. Work on the feature and push updates.
3. Open a pull request (PR) for code review.
4. Merge the PR into `main` and deploy immediately if necessary.

#### Usage
Ideal for small teams and projects with continuous integration and delivery (CI/CD).

### GitLab Flow

![GitLab Flow Diagram](https://res.cloudinary.com/djgwvmcdl/image/upload/v1748952183/6194709048910268705_ltitoo.jpg)

#### Description
A flexible strategy for managing development, staging, and production environments.

#### Branches

- **main / master** – Latest production-ready code.
- **development/** – For ongoing development work.
- **feature/** – For experimental work, merged quickly.
- **environment/** – For managing code in specific environments (e.g., staging, QA, production).

#### Workflow

1. Create a `feature/*` branch for new work.
2. Merge feature branches directly into the appropriate `environment/*` branch.
3. Use merge requests (MRs) for reviews and approvals before merging.
4. Merge from environment branches into `main` for production release when ready.

#### Usage
Works well for projects with multiple deployment environments.

### Trunk-Based Development

![Trunk-Based Development](https://res.cloudinary.com/djgwvmcdl/image/upload/v1748952189/6194709048910268706_cm4rr4.jpg)

#### Description
A minimalist strategy where developers work on a single branch.

#### Branches

- **main / master** – Latest production-ready code.
- **feature/feature-01** – For experimental work, but merged quickly.

#### Workflow

1. Commit changes frequently to `main`.
2. Keep branches short-lived and merge quickly.
3. Use feature flags to deploy incomplete or experimental features safely.

#### Usage
Suitable for fast-moving teams using CI/CD practices.

### Feature Branching

![Feature Branching Diagram](https://res.cloudinary.com/djgwvmcdl/image/upload/v1748952080/6194709048910268703_rsk2ww.jpg)

#### Description
Every feature or bug fix is developed in its own branch.

#### Branches

- **main / master** – Production-ready code.
- **feature/awesome-feature** – For a single feature or bug fix.

#### Workflow

1. Create a branch for a specific feature.
2. Work on the branch until the feature is complete.
3. Merge it back into `main` (or another integration branch).

#### Usage
Suitable for teams working on independent features.

### Forking Workflow

![Forking Workflow Diagram](https://res.cloudinary.com/djgwvmcdl/image/upload/v1748953081/8412cc98-67ce-4399-acab-360484c69620_udzcd1.png)

#### Description
Used in open-source projects where contributors work on their own fork of the repository.

#### Workflow

1. Fork the main repository.
2. Create a branch in your fork for the feature or bug fix.
3. Work on the branch and commit your changes.
4. Submit a pull request to the main repository for review.

#### Usage
Ideal for open-source collaboration.

<br /><br />
