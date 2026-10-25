# About Pull Requests

## 1. What Is a Pull Request?

A **pull request (PR)** is a proposal to merge code changes from one branch into another branch in a GitHub repository. It allows developers to discuss, review, and validate changes before incorporating them into the target branch.

A pull request does not automatically mean that the changes have been merged. The proposed changes may need review, updates, and successful automated checks before merging is allowed.

## 2. Why Use Pull Requests?

Pull requests support collaboration and help teams maintain code quality by allowing developers to:

- Identify bugs and potential problems before changes reach the target branch.

- Discuss proposed changes and provide feedback on specific lines of code.

- Review the differences between the source branch and the target branch.

- Run automated checks, such as tests, builds, and code-scanning tools.

- Maintain a clear history of proposed changes and review discussions.

## 3. Key Parts of a Pull Request

A pull request brings together the information needed to review proposed changes.

- **Conversation:** Contains the pull request description, comments, reviews, and activity history.

- **Commits:** Shows the commits included in the proposed changes.

- **Checks:** Displays the results of automated tests, builds, and other configured validations.

- **Files changed:** Shows the differences between the proposed changes and the target branch. Reviewers can inspect these differences and comment on specific lines.

- **Merge box:** Indicates whether the pull request can be merged and identifies outstanding requirements or merge conflicts that may prevent merging.

## 4. How Pull Requests Fit into the Git Workflow

A typical pull request workflow includes the following steps:

1. **Create or choose a branch:** Work on a separate branch to isolate changes from other development work. A fork may be used when contributing to a repository without directly working on the original repository.

2. **Make and commit changes:** Modify files and create commits that record the changes.

3. **Open a pull request:** Propose merging the changes from the source branch, also called the head branch, into the target branch, also called the base branch.

4. **Review and discuss:** Collaborators inspect the changes, provide feedback, and request updates when necessary.

5. **Run checks and address problems:** Resolve any issues identified during review or automated validation. A merge conflict may also need to be resolved if Git cannot combine the branch changes automatically.

6. **Merge the pull request:** Once the applicable requirements are satisfied and any merge conflicts have been resolved, the changes can be merged into the target branch.

The exact workflow may vary depending on repository settings, branch protection rules, and the team's development process.

## 5. Pull Requests and Merge Conflicts

A pull request proposes integrating changes from one branch into another. Git can often combine the changes automatically, but a **merge conflict** occurs when Git cannot safely determine the final content.

For example, two branches may modify the same line of a file differently, or one branch may delete a file while the other modifies it.

When a merge conflict prevents a pull request from being merged, the conflicting changes must be resolved before the merge can proceed. The developer should inspect the affected files, determine the intended final content, and verify the resolution rather than choosing one version blindly.

Resolving a merge conflict does not necessarily mean that the resulting code is logically correct. The final changes should still be reviewed and tested when appropriate.

## 6. Important Terms

- **Repository:** A project location that contains files and their version history.

- **Branch:** An independent line of development within a repository.

- **Source or head branch:** The branch containing the proposed changes.

- **Target or base branch:** The branch into which the proposed changes are intended to be merged.

- **Commit:** A recorded set of changes in the repository's history.

- **Diff:** A representation of the differences between two versions of files.

- **Merge:** An operation that integrates changes from different development histories.

## 7. Scope and Limitations

This document explains pull requests and their relationship to the Git workflow and merge conflicts. It does not provide complete instructions for every Git command or every type of merge conflict.

For detailed troubleshooting, consult the dedicated knowledge documents about merge conflicts, resolving conflicts from the command line, resolving conflicts on GitHub, and Git command usage.
