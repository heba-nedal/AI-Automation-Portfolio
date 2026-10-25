# Resolving a Merge Conflict on GitHub

## 1. Overview

GitHub allows developers to resolve certain simple merge conflicts directly in a pull request.

This approach is suitable for straightforward conflicts involving competing changes to lines of text. More complex conflicts may require a local repository and command-line tools.

Resolving a conflict on GitHub is not the same as merging the pull request into its base branch.

**Important:** When you resolve conflicts through GitHub's conflict editor, GitHub merges the base branch into the head branch and commits that merge to the head branch. Review the target branch carefully before proceeding.

## 2. When Can You Use the GitHub Conflict Editor?

The conflict editor is suitable for some simple text conflicts where the intended final content is clear.

Use the command line when:

- GitHub does not provide the option to resolve the conflict.

- The conflict requires more complex investigation or editing.

- You need local development tools or tests to verify the changes.

The available options depend on the repository and pull request state.

## 3. Steps to Resolve a Conflict on GitHub

### Step 1: Open the pull request

Open the repository on GitHub, navigate to the **Pull requests** section, and select the pull request that contains the merge conflict.

### Step 2: Open the conflict editor

Near the bottom of the pull request, select **Resolve conflicts**.

If this option is unavailable or disabled, use an appropriate Git client or resolve the conflict from the command line.

### Step 3: Review the conflicting content

GitHub displays the conflicting sections in the affected files. Conflict markers identify the competing versions:

- `<<<<<<<`: Begins one version of the content.

- `=======`: Separates the competing versions.

- `>>>>>>>`: Ends the other version.

Read both versions carefully before deciding what the final content should be.

### Step 4: Choose the intended final content

You can keep one version, combine both versions, or make a different change that preserves the intended behavior.

Remove the conflict markers and any content that should not remain in the final file.

Do not simply remove the markers without reviewing the meaning of the resulting content.

### Step 5: Resolve every conflict in the file

If the file contains multiple conflicting sections, repeat the review and editing process for each section.

When all conflicts in the current file have been resolved, click **Mark as resolved**.

### Step 6: Resolve conflicts in other files

If other files also contain conflicts, select each file and repeat the process.

Resolve all conflicting files before continuing.

### Step 7: Commit the resolution

After all conflicts have been marked as resolved, click **Commit merge**.

This commits the merge of the base branch into the head branch.

### Step 8: Review any branch prompts

GitHub may ask you to confirm the branch being updated or create a new head branch.

A protected head branch may require creating a new branch for the pull request. Follow the repository's displayed instructions and verify the target before confirming.

### Step 9: Complete the pull request merge

After resolving the conflicts, the pull request may become eligible for merging. Review its status and any required checks or approvals.

If the pull request satisfies the repository's requirements, select **Merge pull request** to merge it into the base branch.

Resolving conflicts and merging the pull request are separate steps.

## 4. Verifying the Resolution

Before completing the workflow, check that:

- Every conflicting section has been reviewed.

- All conflict markers have been removed from the resolved content.

- The final content preserves the intended changes.

- Every conflicting file has been marked as resolved.

- The merge was committed to the intended head branch.

- The pull request's remaining checks and requirements have been reviewed.

Removing conflict markers does not guarantee that the resulting code is correct. For code changes, additional testing may be necessary.
