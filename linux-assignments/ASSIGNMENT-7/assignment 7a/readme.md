# Git Assignment 7A

## Objective

This assignment demonstrates Git branching, merging, merge conflicts, and conflict resolution using the **ours** and **theirs** concepts.

## Tasks Completed

1. Created a `ninja` folder at the root level of the repository.
2. Created `ninja/README.md` with the initial content:

   ```text
   Trying fast forward merge
   ```
3. Created a Git branch named `ninja`.
4. Switched to the `ninja` branch.
5. Verified the repository using `git status`.
6. Committed the changes to the `ninja` branch.
7. Merged the `ninja` branch into the `master` branch.
8. Modified `ninja/README.md` in the `master` branch with:

   ```text
   Changes in master branch
   ```
9. Committed the changes in the `master` branch.
10. Switched to the `ninja` branch.
11. Modified `ninja/README.md` in the `ninja` branch with:

    ```text
    Changes in ninja branch
    ```
12. Committed the changes in the `ninja` branch.
13. Merged the `ninja` branch into `master` again to intentionally generate a merge conflict.
14. Resolved the conflict using the **theirs** strategy.
15. The final content from the `ninja` branch overrides the content from the `master` branch.

## Conflict Resolution

During the merge conflict:

* **Ours** refers to the branch currently checked out (`master`).
* **Theirs** refers to the branch being merged (`ninja`).

The conflict was resolved using:

```bash
git checkout --theirs ninja/README.md
git add ninja/README.md
git commit -m "Resolve merge conflict using theirs"
```

Therefore, the final `README.md` contains:

```text
Changes in ninja branch
```

## Verification Commands

```bash
git status
git branch -a
ls -la ninja
cat ninja/README.md
git log --oneline --graph --decorate --all -15
git rev-list --parents -1 HEAD
```

## Result

The assignment successfully demonstrates:

* Git branch creation
* Branch switching
* Git status verification
* Git commits
* Fast-forward merge
* Merge conflict generation
* Conflict resolution
* Ours and theirs concepts
* Merge commit creation
* Ninja branch changes overriding master branch changes

Screenshot 1 – Git status and branches
<img width="900" height="702" alt="image" src="https://github.com/user-attachments/assets/c6a18028-5227-44e5-afe3-bdd87cb0ca7b" />

Screenshot 2 – ninja folder and README content
<img width="900" height="75" alt="image" src="https://github.com/user-attachments/assets/66c9fe0e-ac3b-4a6e-81ea-1d17c0f347b9" />

Screenshot 3 – All branches
<img width="900" height="38" alt="image" src="https://github.com/user-attachments/assets/9d653aff-86f5-4125-8459-758ad2458225" />

Screenshot 4 – Ninja branch commits
<img width="900" height="302" alt="image" src="https://github.com/user-attachments/assets/6dc14ccb-6a55-40c0-b143-39035a269e8d" />

Screenshot 5 – Master branch commits
<img width="900" height="109" alt="image" src="https://github.com/user-attachments/assets/cba56c7b-0cf4-4513-8400-695422d65871" />

Screenshot 6 – Complete Git history
<img width="900" height="68" alt="image" src="https://github.com/user-attachments/assets/f12ee59a-9ca2-4452-a154-bb7ec5bb6468" />






