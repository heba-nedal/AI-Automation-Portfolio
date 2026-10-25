# Merge Conflicts

## 1. What Is a Merge Conflict?

Git allows developers to combine changes from different branches. When changes affect separate lines or files, Git can often merge them automatically.

A **merge conflict** occurs when Git cannot determine how to combine changes safely without human input. This commonly happens when:

- Two branches modify the same line of a file in different ways.
- One branch modifies a file while another branch deletes that file.

A merge conflict does not necessarily mean that the code is incorrect. It means Git needs the developer to decide how the competing changes should be combined.

## 2. Why Do Merge Conflicts Matter?

A merge conflict prevents Git from completing the merge automatically. The conflicting changes must be resolved before the merge can be completed.

In a GitHub pull request, unresolved merge conflicts can prevent the pull request from being merged.

Resolving a conflict means determining the intended final state of the affected files. This may involve keeping one change, combining both changes, or making a different change that preserves the intended behavior.

## 3. Choosing How to Resolve a Conflict

The appropriate method depends on the conflict and the tools available.

### Resolve the conflict on GitHub

GitHub provides a web interface for resolving certain simple conflicts, particularly conflicts involving competing changes to lines of text.

This option can be convenient when the conflict is straightforward and the required final content is clear.

### Resolve the conflict locally

More complex conflicts may require working in a local repository. This allows the developer to inspect the files, use Git commands, edit the affected content, and run relevant tests before pushing the resolution.

For example, a developer may start a merge and receive output similar to this:

```shell
git merge feature-branch
```

```text
Auto-merging styleguide.md
CONFLICT (content): Merge conflict in styleguide.md
Automatic merge failed; fix conflicts and then commit the result.
```

This output indicates that Git could not automatically combine the changes in `styleguide.md`. The developer must inspect and resolve the conflict before completing the merge.

## 4. What Happens After a Conflict Is Resolved?

Resolving the conflicting content is only part of the process. The developer should also:

1. Review the affected files to confirm that the intended changes are present.
2. Check Git's reported repository state.
3. Stage the resolved files.
4. Complete the merge by committing the result when required.
5. Push the resulting changes when working with a remote pull request.
6. Run relevant tests or checks to verify that the combined changes behave as expected.

The exact commands and workflow depend on whether the conflict is being resolved locally or through GitHub's interface.

**Important:** A conflict-free merge does not guarantee that the resulting code is correct. Conflicting changes may be combined incorrectly, or the merged code may introduce bugs. Review and testing are still necessary.

## 5. Common Misunderstandings

- **A merge conflict is not automatically a code error.** It indicates that Git needs help combining changes.
- **Accepting one version is not always the right solution.** Both branches may contain important changes that need to be combined.
- **Removing conflict markers is not sufficient by itself.** The final content must preserve the intended behavior.
- **Resolving the conflict does not necessarily complete the entire workflow.** The changes may still need to be staged, committed, pushed, reviewed, or tested.

## 6. Scope and Limitations

This document focuses on why merge conflicts occur, why they block merging, and how to choose an appropriate resolution approach.

It does not provide a complete procedure for every conflict type. Detailed command-line instructions and GitHub interface steps are covered in the dedicated resolution guides.

The available information may not cover every conflict scenario or recovery procedure. When the knowledge base does not contain sufficient information to answer a question reliably, the assistant should acknowledge this limitation instead of guessing or presenting unsupported instructions.

## Related Knowledge

- About Pull Requests
- Resolving a Merge Conflict Using the Command Line
- Resolving a Merge Conflict on GitHub
- Branches
