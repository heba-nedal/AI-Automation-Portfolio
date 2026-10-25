# Git Commands Cheat Sheet for Merge Conflicts

## 1. Overview

This document provides a quick reference for Git commands commonly used to inspect repository state, investigate changes, resolve merge conflicts, and complete a merge.

The commands should be used according to the current repository state. Before recommending a command, identify what the user is trying to do and inspect any relevant status information.

## 2. Inspecting the Repository

### `git status`

Shows the current branch, modified files, staged changes, and unresolved merge conflicts.

```shell
git status
```

**When to use it:** Start here when diagnosing a merge conflict. It helps identify which files need attention and whether the merge is still in progress.

### `git diff`

Shows changes that have not been staged.

```shell
git diff
```

**When to use it:** Review unstaged changes before adding them to the staging area.

### `git diff --cached`

Shows changes that have already been staged.

```shell
git diff --cached
```

**When to use it:** Review the exact changes prepared for the next commit, including a conflict resolution.

### `git branch`

Lists local branches and indicates the current branch.

```shell
git branch
```

**When to use it:** Check which local branches are available before starting a branch-related operation.

### `git switch`

Changes the current branch.

```shell
git switch feature-branch
```

**When to use it:** Move to an existing local branch when the repository state permits switching.

Replace `feature-branch` with the intended branch name. Do not assume that switching branches is appropriate while unresolved conflicts or other constraints remain.

## 3. Merging Branches

### `git merge`

Combines changes from another branch into the current branch.

```shell
git merge main
```

**When to use it:** Merge `main` into the current branch, provided that this is the intended operation.

The current branch is the destination of the merge. For example, if the current branch is `feature-branch`, this command attempts to merge `main` into `feature-branch`.

Git may complete the merge automatically or report conflicts that require manual resolution.

### `git merge --abort`

Attempts to abort an in-progress merge and return to the state before the merge began.

```shell
git merge --abort
```

**When to use it:** When a merge is in progress and the user explicitly wants to abandon it.

**Important:** Aborting a merge can be affected by changes that existed before the merge began. If there were uncommitted changes when the merge started, Git may not be able to reconstruct the exact original state. Inspect the repository and explain the risks before recommending this command.

## 4. Handling a Deleted File Conflict

### `git rm`

Stages the removal of a file from the repository.

```shell
git rm README.md
```

**When to use it:** When a deleted-file conflict has been reviewed and the intended resolution is to keep the file deleted.

If the intended resolution is to keep the file, review or restore its intended content and stage it with `git add README.md` instead. Do not decide based only on the status message.

## 5. Staging, Committing, and Pushing

These operations serve different purposes.

### `git add`

Stages changes for the next commit.

```shell
git add styleguide.md
```

Use it after reviewing the resolved file. Prefer naming the specific file to avoid staging unrelated changes.

### `git commit`

Records staged changes in a new commit.

```shell
git commit -m "Resolve merge conflict"
```

After all conflicts are resolved and the relevant files are staged, this can complete the merge.

### `git merge --continue`

Continues an in-progress merge after conflicts have been resolved and staged.

```shell
git merge --continue
```

Use this only when a merge is in progress. It is an alternative to using `git commit` to finish that merge; do not run both to finish the same merge.

### `git push`

Uploads local commits to a remote repository.

```shell
git push
```

Use it after committing when the remote branch needs to be updated. Pushing does not itself resolve conflicts.

### Choosing the Correct Command

Do not recommend a command based only on the fact that a merge conflict occurred. First identify the current repository state and the user's intended action.

| Situation | Appropriate guidance |
|---|---|
| The user needs to inspect unresolved conflicts or repository status | Start with `git status`. |
| The user needs to review unstaged changes | Use `git diff`. |
| The user needs to review staged changes | Use `git diff --cached`. |
| The user has resolved a specific file and verified its content | Stage that file with `git add filename`. |
| A merge is in progress and all conflicts are resolved and staged | Use `git merge --continue` or `git commit`, as appropriate to the current state. Do not run both just to finish the same merge. |
| The user explicitly wants to abandon an in-progress merge | Consider `git merge --abort` only after checking the repository state and explaining potential risks to pre-existing changes. |
| The user needs to upload completed local commits | Use `git push` when appropriate. |

Replace `filename` with the actual path of the resolved file.

If the repository state is unknown, ask the user to share the relevant `git status` output before recommending a state-dependent command. Do not assume that the merge is still in progress or that all conflicts have been resolved.

These recommendations are a guide, not a command sequence to execute blindly. The intended resolution and the current repository state determine the appropriate next step.

## 6. Typical Conflict-Resolution Workflow

1. Inspect the repository with `git status`.
2. Review the conflicting files and understand both versions.
3. Edit each file to produce the intended final content.
4. Stage the specific resolved files with `git add`.
5. Review staged changes with `git diff --cached`.
6. Run relevant tests or checks when applicable.
7. Confirm no unresolved paths remain with `git status`.
8. Finish the merge with either `git commit` or `git merge --continue`, as appropriate.
9. Push the resulting commit if the remote pull request needs to be updated.

This is a general workflow, not a sequence to run blindly. The correct steps depend on the repository state and conflict type.

## 7. Common Mistakes and Limitations

- Staging changes before reviewing the resolved content.
- Using `git add .` without checking whether unrelated changes will be staged.
- Confusing staging, committing, and pushing.
- Assuming that pushing resolves conflicts.
- Running `git merge --abort` without understanding the current merge state and potential impact on local changes.
- Committing before all conflicts have been resolved.
- Assuming a successful merge guarantees correct application behavior.

This cheat sheet is not a complete Git command reference. If the knowledge base does not contain enough information to recommend a command or recovery procedure reliably, the assistant should acknowledge that limitation instead of guessing.
