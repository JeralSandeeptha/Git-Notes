# Cherry Picking

If we want to get specific commits instead of merging branches we can use `Cherry Picking`

Then we can selectively gets updates / commits from another branches as out wish

<br/>

**Basic Command:**

```git
git cherry-pick <commit-hash>
```

<br/>

## 📝 Cherry-Pick Commands

**Append Origin Note:** Automatically adds the original commit tracking note

```git
git cherry-pick -x <commit-hash>
```

<br/>

**Edit Message & Note:** Opens your text editor to modify the message while still keeping the trace note

```git
git cherry-pick -x -e <commit-hash>
```

<br/>

**Cherry-Pick Range with Notes:** Appends tracking notes for a sequence of commits (excluding A, up to and including B)

```git
git cherry-pick -x <commit-A> <commit-B>
```

<br/>

## 🛑 Handling Conflicts

If the cherry-pick process halts due to merge conflicts, Git flags the problem areas and sets a temporary CHERRY_PICK_HEAD reference. Resolve it using these commands:

1. Open files and clear the standard <<<<<<< and >>>>>>> conflict markers

2. Staged those new changes

```git
git add <file-path>
```

3. Finalize the cherry-pick to complete the commit

```git
git cherry-pick --continue
```

If we want to stop (Alternative) / give up and return your branch to its original state:

```git
git cherry-pick --abort
```
