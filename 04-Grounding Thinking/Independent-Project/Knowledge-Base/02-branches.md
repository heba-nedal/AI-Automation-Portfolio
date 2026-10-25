# Branches in Git

## 1. What Is a Branch?

A branch is an independent line of development in a Git repository. Developers use branches to work on features, fix bugs, or experiment without immediately changing the work on another branch.

A branch is created from an existing branch. For example, a developer might create a feature branch from `main`, make changes on that branch, and later propose merging those changes into `main`.

Branches help developers work independently, but changes made on different branches may need to be reconciled when the branches are merged.

## 2. Base Branch and Head Branch

When working with a pull request, two important terms are:

- **Base branch:** The branch into which the proposed changes will be merged. It is often `main`.

- **Head branch:** The branch containing the proposed changes. It is often a feature branch.

For example, in a pull request from `feature-login` into `main`:

- Base branch: `main`

- Head branch: `feature-login`

A pull request compares the proposed changes on the head branch with the base branch.

Understanding these branches helps identify which changes are being introduced and which existing changes must be considered during a merge.

## 3. Keeping Branches in Sync

Suppose a developer creates `feature-login` from `main`. While the developer works on the feature, other changes may be merged into `main`.

The two branches can then contain different changes. Merging the updated base branch into the feature branch can help the developer integrate those changes and discover conflicts before the feature is merged.

For example:

```shell
git switch feature-login
git merge main
```

This example assumes that the local repository has the relevant branches and that the developer intends to merge `main` into `feature-login`.

Git may complete the merge automatically, or it may report conflicts that require manual resolution.

The appropriate workflow depends on the repository state and the team's practices.

## 4. How Branches Relate to Merge Conflicts

Merge conflicts can occur when Git cannot automatically reconcile changes from different branches.

For example:

- Both branches modify the same line differently.

- One branch modifies a file while another deletes it.

- Changes made on the base branch affect files also modified on the head branch.

The existence of two branches does not itself mean a conflict exists. Git can often combine changes automatically.

When a conflict occurs, the developer must determine the intended final content before completing the merge.

A pull request that cannot be merged does not necessarily have a merge conflict. The assistant should distinguish an actual conflict from other possible reasons a merge is blocked, using only the information available in the knowledge base.

## 5. Scope and Limitations

This document explains branches, base and head branches, and how branches relate to merge conflicts.

It does not cover every branch-management command or merge strategy. Detailed conflict diagnosis and resolution procedures are covered in the dedicated resolution guides.

When the available knowledge base does not contain enough information to answer a question reliably, the assistant should acknowledge that limitation instead of guessing.

## Related Knowledge

- About Pull Requests

- Merge Conflicts

- Resolving a Merge Conflict Using the Command Line

- Resolving a Merge Conflict on GitHub
