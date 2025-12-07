---
title: "GitHub Related"
date: 2025-12-06
description: "Add description"
summary: "GitHub"
tags: []
---

### Branch Merge Workflow: Merging `dev` into `main`

---

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

When Do Merge Conflicts Occur?
- **Case 1** 
  - step 1: create `dev` from `main`
  - step 2: make changes only in `dev` (no changes in `main`)
  - step 3: `dev` → `main`

  Result: No conflicts.

- Case 2
  - step 1: create `dev` from `main`
  - step 2: make changes only in `main` (no changes in `dev`)
  - step 3: `dev` → `main`

  Result: No conflicts.

- Case 3
  - step 1: create `dev` from `main`
  - step 2: make changes in both `dev` and `main`
  - step 3: merge `dev` → `main`

  Result: Conflicts occur **only if** both branches modify the **same or overlapping lines**. Otherwise, no conflict.


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

### Git Terminology: Repositories, Remotes, and Branches

#### Repository

- **Local repository**: the Git repository stored on your computer
- **Remote repository**: the Git repository stored on a server (e.g., GitHub). Your local Git refers to each remote repository using a **remote name** (default: `origin`)


#### Branch

- **Local branch**: a branch in your local repository (e.g., `dev`)
- **Remote branch**: a branch in the remote repository, represented locally as `<remote-name>/<branch-name>` (e.g., `origin/main`, `origin/dev`)

#### Names

- **Repository name**: 
  - **Local repository name**: The folder name on your computer (e.g., `myproject/`). Not important for Git’s internal operations.
  - **Remote repository name**: The actual name of the project on GitHub (e.g., `myproject`).

- **Remote name**: a local nickname Git uses to refer to a remote repository URL (default: `origin`). It does not have to match the remote repository name.

- **Branch name**:
  - **Local branch name**: name of a branch in the local repository (e.g., `dev`).
  - **Remote branch name**: name of a branch in the remote repository, represented as `<remote-name>/<branch-name>` (e.g., `origin/main`, `origin/dev`)


```mermaid
flowchart TD

A[Start: Local Repository] --> B[Create dev branch<br>git switch -c dev]
B --> C[Push branch to remote<br>git push -u origin dev]

C --> D[Make changes on dev<br>Edit files<br>git add .<br>git commit -m ...]
D --> E[Push updates<br>git push]

E --> F[Switch to main<br>git switch main]
F --> G[Update main<br>git pull]

G --> H[Merge dev into main<br>git merge dev]

H --> I{Conflicts?}

I -- No --> J[Push merged result<br>git push]

I -- Yes --> K[Resolve conflicts<br>Fix files<br>git add<br>git commit]
K --> J

J --> L[(Optional) Clean up dev<br>git branch -d dev<br>git push origin --delete dev]
```