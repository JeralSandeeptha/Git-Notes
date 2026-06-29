# Merging

- `Merging` in Git is the process of combining changes from one branch into another — most commonly, from a `feature branch` into `main` / `child branch` into `parent branch`.

```cmd
# Step 1: Switch to the branch you want to merge into (usually main)
git checkout main

# Step 2: Merge the other branch into this one
git merge feature-x
```

- There are several ways to merge branches:
  - `Merge`
  - `Rebase`

- `Merge` option, it also requires a commit to it's parent for merge. If there are many commits those commits combine into single commit and merge as a single commit.
![Merge](https://res.cloudinary.com/djgwvmcdl/image/upload/v1748893501/492bbdd4d1c256ad4b07c9a042fd18fca353b1cc_eb1o91.png)

- `Rebase` option, replays changes from one line of work onto another in the order they were introduced, whereas merging takes the endpoints and merges them together.
![Rebase](https://res.cloudinary.com/djgwvmcdl/image/upload/v1748893771/1_mQOZjM3wwL1UV-ydQYAJTg_ieqpln.webp)
