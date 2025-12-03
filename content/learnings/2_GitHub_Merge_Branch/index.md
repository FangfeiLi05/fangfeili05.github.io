---
title: "Branch Merge"
date: 2025-12-03
description: "Add description"
summary: "GitHub"
tags: []
---

#### Merge dev branch into main

**Step 1. Run**
```
git switch main   # Switch to the main branch
git pull          # Update main (local branch) with the newest code from the remote repository
git merge dev     # Merge the dev branch into main
```

**Step 2. Conflicts?**

- ❌ **If NO conflicts:** Skip to `Step 3`
- ✅ **If YES:** Resolve
  ```
  git status # Check which files have conflicts
  ```

  You will see conflicted files (e.g. `src/app.js`).

  Open the file (e.g. `src/app.js`) you will see something like:
  ```
  <<<<<<< HEAD
  content from main branch
  =======
  content from dev branch
  >>>>>>> dev
  ```
  Replace the entire block above with `the final version you want` (this can be main version, dev version, or a custom combined version).

  Then run
  ```
  git add src/app.js                                  # Stage the resolved file
  git commit -m "Resolve merge conflicts in app.js"   # Commit the fix
  ```

**Step 3. Push the merged result**
```
git push
```

**Step 4. (Optional) Clean up the dev branch**
```
git branch -d dev.             # Delete the local dev branch
git push origin --delete dev   # Delete the remote dev branch
```