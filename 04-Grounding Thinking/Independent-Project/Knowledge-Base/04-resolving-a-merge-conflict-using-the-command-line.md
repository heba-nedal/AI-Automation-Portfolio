# Resolving a Merge Conflict Using the Command Line

## 1. Overview

A merge conflict occurs when Git cannot automatically combine changes from different branches. Common examples include:

- **Competing line changes:** Two branches modify the same part of a file differently.

- **Deleted file conflicts:** One branch deletes a file while another branch modifies it.

Git may also report other conflict types, such as rename/delete conflicts or conflicts involving binary files. Their resolution depends on the specific situation and may require additional investigation.

This guide explains how to diagnose and resolve competing line changes and deleted file conflicts using the command line.

## 2. Before You Start

Open a terminal or Git Bash and navigate to the local repository containing the conflict.

```shell
cd REPOSITORY-NAME
```

Check the repository state:

```shell
git status
```

Git reports the affected files and indicates whether there are unresolved paths.

For example:

```text
On branch feature-branch
You have unmerged paths.
Unmerged paths:
  both modified:   styleguide.md
```

In this example, `styleguide.md` has competing modifications that require resolution.

**Important:** Read the complete `git status` output before proceeding. If the repository contains unrelated changes, preserve them and avoid staging them accidentally.

## 3. Resolving Competing Line Changes

This conflict occurs when two branches make incompatible changes to the same lines of a file.

### Step 1: Open the conflicted file

Open the file identified by `git status` in a text editor.

Git typically marks conflicting sections with three markers:

- `<<<<<<<`: Begins one version of the conflicting content.

- `=======`: Separates the two versions.

- `>>>>>>>`: Ends the other version and identifies the corresponding branch or commit.

For example:

```text
If you have questions, please
<<<<<<< HEAD
open an issue
=======
ask your question in IRC.
>>>>>>> branch-a
```

`HEAD` represents the version from the current branch in this example. The other section contains the competing change.

### Step 2: Decide on the final content

Read both versions and determine which changes should remain.

Possible approaches include:

- Keep the current branch's change.

- Keep the incoming branch's change.

- Combine both changes.

- Write a different version that preserves the intended behavior.

For example, if both suggestions are useful, the final content might be:

```text
If you have questions, please open an issue or ask your question in IRC.
```

This is only an example. The correct resolution depends on the meaning and requirements of the actual code or document.

### Step 3: Remove the conflict markers

Edit the file so that it contains only the intended final content.

Remove the `<<<<<<<`, `=======`, and `>>>>>>>` markers and any unwanted conflicting content. Do not simply delete the markers while leaving an incorrect combination of changes.

### Step 4: Stage the resolved file

After reviewing the file, stage that specific file:

```shell
git add styleguide.md
```

Replace `styleguide.md` with the actual filename.

Staging the specific file is safer than using `git add .`, which may also stage unrelated changes.

### Step 5: Review the staged changes

Inspect the staged changes:

```shell
git diff --cached
```

Confirm that the final content is correct and that unrelated changes have not been included.

## 4. Resolving a Deleted File Conflict

A deleted file conflict occurs when one branch deletes a file while another branch modifies it.

For example, Git may report:

```text
Unmerged paths:
  deleted by us:   README.md
```

The wording may differ depending on which branch performed the deletion.

### Step 1: Decide whether to keep or delete the file

Consider why the file was deleted and whether the modifications made on the other branch are still needed.

There are two main outcomes.

### Option A: Keep the file

If the file should remain in the repository, restore or edit its intended content as needed, then stage it:

```shell
git add README.md
```

Review the file before staging it to ensure that the desired changes are preserved.

### Option B: Delete the file

If the deletion is intentional and the file should no longer exist, use:

```shell
git rm README.md
```

This stages the file's removal.

**Important:** Do not choose between keeping and deleting a file based only on Git's status message. The correct decision depends on the project's intended behavior and the purpose of the file.

## 5. Verifying the Resolution

Resolving the visible conflict is not enough. Verify that Git recognizes the resolution and that the resulting content is correct.

### Step 1: Check the repository state

Run:

```shell
git status
```

Review the output for remaining unmerged paths. If other files are still unresolved, repeat the appropriate resolution process for those files.

### Step 2: Inspect the final content

Review each resolved file carefully.

For text files, check for leftover conflict markers:

```text
<<<<<<<
=======
>>>>>>>
```

These markers should not remain as unresolved conflict markers in the final content. However, their absence alone does not prove that the resolution is correct.

### Step 3: Review the staged changes

Run:

```shell
git diff --cached
```

Confirm that the staged changes represent the intended resolution and do not include unrelated modifications.

### Step 4: Run relevant tests and checks

If the repository contains automated tests, run the relevant tests. For code changes, verify that the combined changes still behave as expected.

A successful Git merge does not guarantee that the resulting code is free of bugs.

### Step 5: Confirm that all conflicts are resolved

Run:

```shell
git status
```

If the merge is still in progress, all conflicts must be resolved and staged before the merge can be completed.

When the output indicates that all conflicts are resolved, proceed with the merge workflow.

## 6. Completing the Merge

After resolving all conflicts, review the affected files, stage the resolved files, and verify that no unresolved paths remain.

### Step 1: Check the repository state

Run:

```shell
git status
```

Confirm that all conflicts have been resolved and that the repository is still in the expected merge state.

### Step 2: Review the staged changes

Run:

```shell
git diff --cached
```

Verify that the staged content represents the intended resolution and does not include unrelated changes.

### Step 3: Complete the merge

When a merge is in progress and all conflicts have been resolved and staged, use the command appropriate to the current repository state.

Option A:

```shell
git merge --continue
```

This continues the in-progress merge.

Option B:

```shell
git commit
```

This can complete the merge by creating the merge commit when Git is waiting for that commit.

**Important:** These are alternative ways to complete the same merge in the appropriate context. Do not run both commands simply to finish the same merge. If Git reports that the merge is not in progress or that additional steps are required, inspect the output and repository state before proceeding.

### Step 4: Verify the result

Run:

```shell
git status
```

Confirm that no unresolved conflicts remain and check whether the merge has completed.

### Step 5: Update the remote branch when appropriate

If the resolved merge needs to be shared with a remote repository, push the resulting commit:

```shell
git push
```

Pushing uploads local commits; it does not resolve conflicts by itself.

If the merge is part of a GitHub pull request, review the pull request's status, required checks, and approvals. Resolving conflicts does not automatically mean the pull request has been merged into its base branch.

## 7. When the Conflict Cannot Be Resolved Using This Guide

This guide covers competing line changes and deleted file conflicts. Other situations may involve renamed files, binary files, submodules, or more complex interactions between branches.

The correct resolution depends on the type of conflict and the repository state. Do not apply the procedures in this guide blindly to a different conflict type.

If the available knowledge base does not contain enough information to diagnose or resolve the specific problem reliably, acknowledge that limitation instead of inventing commands or recovery steps.

## 8. Common Mistakes to Avoid

- Choosing one version without understanding the competing changes.

- Removing conflict markers without reviewing the resulting content.

- Using `git add .` without checking whether unrelated changes will be staged.

- Assuming that the absence of visible conflict markers proves the code is correct.

- Committing before all unmerged paths have been resolved.

- Running destructive recovery commands without understanding their effects on local work.

## Related Knowledge

- About Pull Requests

- Branches in Git

- Merge Conflicts

- Resolving a Merge Conflict on GitHub

- Git Commands Cheat Sheet
