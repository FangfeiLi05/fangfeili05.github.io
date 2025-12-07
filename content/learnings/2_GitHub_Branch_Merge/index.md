---
title: "GitHub Related"
date: 2025-12-06
description: "Add description"
summary: "GitHub"
tags: []
---

### Branch Merge Workflow: Merging `dev` into `main`


{{< mermaid >}}
graph LR;
A[Lemons]-->B[Lemonade];
B-->C[Profit]
{{< /mermaid >}}




#### Step 1. Create a new `dev` branch
```bash
git switch -c dev        # Create and switch to the dev branch
git push -u origin dev   # Push dev to remote and set upstream (first push only)
```

#### Step 2. Make changes on the `dev` branch
Edit your files normally, then stage and commit:
```bash
git add .
git commit -m "Your commit message"
```

Push updates to the remote:
```bash
git push   # Push to origin/dev (since upstream is set)
```

#### Step 3. Merge dev into main
```bash
git switch main   # Switch to the main branch
git pull          # Update main (local branch) with the newest code from the remote repository, to ensure main is up-to-date
git merge dev     # Merge the dev branch into main
```

#### Step 2. Handle merge conflicts (if any)

If No Conflicts, skip to `Step 5`.

If conflicts exist, resolve them:
```bash
git status   # Shows files with conflicts
```

Conflicted files (e.g. `src/app.js`) will be shown.

Open the file (e.g. `src/app.js`) to see a conflict block like this:
```bash
<<<<<<< HEAD
content from main branch
=======
content from dev branch
>>>>>>> dev
```
Replace the entire block with **the final version you want** (can be main version, dev version, or a custom combined version).

Then:
```bash
git add src/app.js
git commit -m "Resolve merge conflicts in app.js"   # Commit the fix
```

#### Step 5. Push the merged result
```bash
git push
```

#### Step 6. (Optional) Clean up `dev`
```bash
git branch -d dev.             # Delete local dev branch
git push origin --delete dev   # Delete remote dev branch
```

---

### When Do Merge Conflicts Occur?

| &nbsp; | Conditions | Result |
| ----- | ----- | ----- |
| **Case 1** | 1. Create `dev` from `main` <br> 2. Changes only in `dev` (none in `main`) <br> 3. Merge `dev` → `main` | **No conflicts** |
| **Case 2** | 1. Create `dev` from `main` <br> 2. Changes only in `main` (none in `dev`) <br> 3. Merge `dev` → `main` | **No conflicts** |
| **Case 3** | 1. Create `dev` from `main` <br> 2. Changes in **both** `dev` and `main` <br> 3. Merge `dev` → `main` | Conflicts occur **only if** both branches <br> modify **the same or overlapping lines**. <br> Otherwise, **no conflict**. |

---

### Git Terminology: Repositories, Remotes, and Branches

|   | Local | Remote |
| ----- | ----- | ----- |
| **Repository** | **Local repository:** the Git repository stored on your computer. <br> **Local repository name:** the folder name on your computer. Not important for Git internals. | **Remote repository:** the Git repository stored on a server (e.g., GitHub). <br> **Remote repository name:** actual project name on GitHub (e.g., `myproject`). <br> Accessed via a **remote name** (default: `origin`). <br> **Remote name:** a local nickname for a remote repository URL (default: `origin`). It does **not** have to match the repository name. |
| **Branch**  | **Local branch:** branch in your local repo (e.g., `dev`). <br> **Local branch name:** name of that local branch. | **Remote branch:** branch stored in the remote repo, shown as `<remote-name>/<branch-name>` (e.g., `origin/main`, `origin/dev`). <br> **Remote branch name:** name of that remote branch (same representation). |

