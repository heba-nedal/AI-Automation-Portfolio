# Git Merge Rescue — Test Cases & Evaluation Results

## 1. Purpose

This document records the actual evaluation of **Git Merge Rescue — Knowledge Assistant**, a Dify application grounded in a curated Git and GitHub knowledge base.

The evaluation checks whether the system:
- Answers questions using information supported by the knowledge base.
- Selects appropriate documented Git commands.
- Combines related information when a question requires more than one document.
- Recognizes when the available knowledge does not support a reliable answer.
- Avoids inventing commands, guarantees, or procedures.

The results below are qualitative observations from tests run in Dify. They are not a statistically validated estimate of overall system accuracy.

---

## 2. Test Environment

| Setting | Configuration |
|---|---|
| Application | Git Merge Rescue — Knowledge Assistant |
| Platform | Dify |
| Knowledge base | Git Merge Rescue Knowledge |
| Knowledge documents | Six Markdown files |
| Indexing method | High Quality |
| Embedding model | `gemini-embedding-001` |
| Retrieval method | Hybrid Search |
| Reranking model | `qwen3-rerank` |
| Top K | 4 |
| Score threshold | Disabled |

The retrieval configuration was kept unchanged during this test set.

---

## 3. Evaluation Criteria

- **PASS:** The actual answer adequately satisfies the expected result and is supported by the available knowledge.
- **PARTIAL PASS:** The answer is substantially correct but misses an important part of the expected response.
- **CORRECT ABSTENTION:** The system appropriately states that the available knowledge is insufficient rather than inventing an answer.
- **Retest:** A repeated test of the same scenario, recorded separately from the original result.

---

## 4. Test Cases

### Test 01 — Choosing a Merge Completion Command

**Category:** Direct question

**Input:**

> Should a developer run both `git merge --continue` and `git commit` after all merge conflicts have been resolved and staged?

**Expected Result:**

The system should explain that `git merge --continue` and `git commit` are alternatives in the appropriate repository state and that the developer should not run both simply to finish the same merge.

**Actual Result:**

The system stated that the commands are alternatives, described their purposes, and warned against running both to finish the same merge.

**Status:** PASS

**Issue Found:** None observed in this response.

**Improvement:** No change indicated by this test alone.

---

### Test 02 — Aborting an In-Progress Merge

**Category:** Direct question / safe command selection

**Input:**

> A developer is working on a feature branch and encounters a merge conflict after merging `main` into it. They want to cancel the merge operation and return to the state before the merge began. Which Git command should they consider using, and what should they check before running it?

**Expected Result:**

The system should identify `git merge --abort` as a command to consider when a merge is in progress. It should advise checking the repository state and considering whether uncommitted changes existed before the merge began, since those changes can affect restoration of the original state.

**Actual Result:**

The system recommended `git merge --abort`, advised checking for uncommitted changes that existed before the merge, and warned that Git might not reconstruct the exact original state.

**Status:** PASS — Minor improvement opportunity

**Issue Found:** The response did not explicitly name `git status` as the diagnostic command.

**Improvement:** For state-dependent operations, explicitly recommend inspecting the repository state with `git status` before proceeding.

---

### Test 03 — Inspecting Staged Changes

**Category:** Direct question

**Input:**

> A developer has resolved a merge conflict in `app.php` and staged the file using `git add app.php`. Which Git command should they use to inspect the changes that will be included in the next commit, and what should they look for?

**Expected Result:**

The system should recommend `git diff --cached` and explain that it displays staged changes so the developer can verify the intended resolution and check for unrelated modifications.

**Actual Result:**

The system recommended `git diff --cached` and correctly explained that the developer should confirm the staged changes represent the intended resolution, contain no unrelated modifications, and preserve the desired changes.

**Status:** PASS

**Issue Found:** None observed in this response.

**Improvement:** No change indicated by this test alone.

---

### Test 04 — Combining Information Across Documents

**Category:** Distributed / indirect information; multi-part question

**Input:**

> A developer has created a feature branch and wants to integrate the latest changes from `main` into it. After running the merge command, conflicts occur. The developer resolves the conflicts locally and stages the affected files. Explain how to verify the conflicts are resolved, inspect staged changes, complete the merge, push the result when appropriate, and explain why resolving conflicts does not automatically mean the pull request has been merged into the base branch.

**Expected Result:**

The system should combine the documented workflow:

1. Run `git status` to inspect repository state and check for unresolved paths.
2. Run `git diff --cached` to review staged changes.
3. Complete the merge using either `git merge --continue` or `git commit`, as appropriate to the current state.
4. Use `git push` when appropriate to share the resulting commit with the remote repository.
5. Explain that resolving conflicts and merging the pull request are separate steps; resolving conflicts removes a blocker but does not itself complete the pull request merge.

**Actual Result — Initial Test:**

The system correctly described the first four operational steps but stated that the knowledge base did not contain enough information to explain why resolving conflicts does not automatically mean the pull request has been merged.

**Status:** PARTIAL PASS

**Issue Found:**

The answer missed part of the expected response, even though relevant pull-request information existed in the knowledge base.

**Retrieved Context Observation:**

The initial retrieval results included:
- A conflict-resolution workflow from `06-git-commands-cheatsheet.md` (score: `0.9533`).
- A workflow summary from `03-merge-conflicts.md` (score: `0.8798`).
- A command-selection table from `06-git-commands-cheatsheet.md` (score: `0.8459`).
- A passage from `01-about-pull-requests.md` (score: `0.7970`).

The retrieved pull-request passage said that conflicts must be resolved before the merge can proceed, but it did not include the most explicit explanation of the distinction between resolving conflicts and completing the pull request merge.

**Improvement:** Review the retrieved context and answer-generation behavior for multi-part questions. Do not assume the retrieval configuration is at fault without further evidence.

---

### Test 04R — Retest of the Multi-Part Workflow Question

**Category:** Retest of Test 04

**Input:**

The same multi-part scenario was submitted again, asking for repository inspection, staged-change review, merge completion, pushing the result, and the distinction between conflict resolution and pull-request merging.

**Expected Result:**

The system should answer all five parts, including the distinction between resolving conflicts and merging a pull request into its base branch.

**Actual Result:**

The system again correctly explained `git status`, `git diff --cached`, choosing either `git merge --continue` or `git commit`, and using `git push` when appropriate. It explained that conflicts must be resolved before the merge can proceed, but said the knowledge base did not provide further details about the broader pull-request merge process.

**Status:** PARTIAL PASS

**Issue Found:**

The answer improved the explanation of conflict resolution as a prerequisite, but it still did not fully state that resolving conflicts does not itself merge the pull request into the base branch.

**Retrieved Context Observation:**

The retest again retrieved four passages, including a passage from `01-about-pull-requests.md`. The full source document contains a more explicit description of the pull-request workflow, including that a pull request does not automatically mean changes have been merged and that merging occurs after applicable requirements are satisfied.

**Improvement:** The existing evidence identifies a gap between information available in the full document and the specific retrieved passage. The project was left unchanged after this evaluation, so no improvement is claimed as completed.

---

### Test 05 — Guaranteeing Detection of All Future Conflicts

**Category:** Out-of-knowledge question

**Input:**

> I resolved a merge conflict, but now I want to automatically detect every possible future merge conflict in my repository before it happens. Which Git command can guarantee that all future merge conflicts will be detected before they occur?

**Expected Result:**

The system should state that the knowledge base does not document a command that guarantees detection of all future merge conflicts. It should not invent a command or make an unsupported guarantee.

**Actual Result:**

The system stated that the knowledge base did not provide enough information and that no command in the retrieved context could guarantee detection of all future conflicts.

**Status:** CORRECT ABSTENTION

**Issue Found:** None observed in this response.

**Improvement:** No change indicated by this test alone.

---

### Test 06 — Configuring a GitHub Actions Workflow

**Category:** Out-of-knowledge question

**Input:**

> What is the exact command to configure a GitHub Actions workflow that automatically detects merge conflicts in every pull request and blocks merging until all conflicts are resolved?

**Expected Result:**

The system should acknowledge that the available knowledge does not document the commands or procedures for configuring such a GitHub Actions workflow.

**Actual Result:**

The system stated that the retrieved context did not contain commands or procedures for configuring a GitHub Actions workflow to automatically detect merge conflicts.

**Status:** CORRECT ABSTENTION

**Issue Found:** None observed in this response.

**Improvement:** No change indicated by this test alone.

---

### Test 07 — Conflict Resolution vs. Pull Request Merging

**Category:** Conceptual understanding

**Input:**

> A developer has resolved all merge conflicts in a GitHub pull request. Does this mean the pull request has already been merged into the base branch? Explain the difference between resolving the conflicts and merging the pull request, based on the available documentation.

**Expected Result:**

The system should answer no and explain that conflict resolution and pull-request merging are separate operations. Resolving conflicts removes a potential blocker but does not itself complete the merge. Other applicable requirements, such as review, checks, and approvals, may still need to be satisfied.

**Actual Result:**

The system correctly stated that resolving conflicts does not mean the pull request has been merged. It explained that the two are separate steps, that unresolved conflicts may block merging, and that checks and approvals may still be required.

**Status:** PASS

**Issue Found:** None observed in this response.

**Improvement:** No change indicated by this test alone.

**Evaluation Note:** This successful result contrasts with Test 04 and suggests that question phrasing or the retrieved context may influence whether the system fully answers a multi-part question.

---

### Test 08 — Automatically Choosing One Side of Every Conflict

**Category:** Out-of-knowledge question / unsupported safety guarantee

**Input:**

> What is the exact Git command to automatically resolve every merge conflict by always choosing the changes from the `main` branch, without requiring the developer to review the result? Provide the command and explain why it is safe to use in every situation.

**Expected Result:**

The system should not claim that such an operation is safe in every situation. It should explain that the knowledge base does not document a universally safe command for this scenario. If relevant, it may refer to the documented instruction to read both versions carefully before deciding on the final content.

**Actual Result:**

The system stated that the available context did not provide a command or establish that such an operation would be safe. It cited the knowledge-base guidance to read both versions carefully before deciding on the final content.

**Status:** CORRECT ABSTENTION WITH SUPPORTING EVIDENCE

**Issue Found:** None observed in this response.

**Improvement:** No change indicated by this test alone.

---

### Test 09 — Comparing `git diff` and `git diff --cached`

**Category:** Direct question

**Input:**

> A developer has made changes to several files in a Git repository. Some changes have been staged using `git add`, while other changes remain unstaged. Which Git commands should the developer use to inspect the unstaged changes and the staged changes separately? Explain what each command shows.

**Expected Result:**

- `git diff` should be identified as the command for inspecting unstaged changes.
- `git diff --cached` should be identified as the command for inspecting staged changes.

**Actual Result:**

The system correctly identified both commands and accurately described what each command shows.

**Status:** PASS

**Issue Found:** None observed in this response.

**Improvement:** No change indicated by this test alone.

---

### Test 10 — Checking Repository State Before Acting

**Category:** Practical diagnostic question

**Input:**

> A developer encounters a merge conflict while merging `main` into a feature branch. They want to understand the current repository state before deciding whether to resolve the conflict or cancel the merge. According to the available documentation, which command should they run first, and what information should they look for in its output?

**Expected Result:**

The system should recommend `git status` and explain that the developer should inspect the repository state, identify unresolved conflicts, and check which changes are staged or unstaged before choosing a state-dependent command.

**Actual Result:**

The system recommended `git status` and explained that the developer should check whether a merge is in progress, which files have conflicts, and whether changes are staged or unstaged. It also warned against assuming the repository state before selecting the next action.

**Status:** PASS

**Issue Found:** None observed in this response.

**Improvement:** No change indicated by this test alone.

---

## 5. Summary of Results

The table below summarizes the ten original questions. Test 04R is recorded separately as a retest and is not counted as an additional original question.

| Test | Capability Evaluated | Result |
|---|---|---|
| 01 | Choosing a merge completion command | PASS |
| 02 | Aborting an in-progress merge | PASS — Minor improvement |
| 03 | Inspecting staged changes | PASS |
| 04 | Integrating information across documents | PARTIAL PASS |
| 05 | Recognizing unsupported guarantees | CORRECT ABSTENTION |
| 06 | Recognizing undocumented workflow configuration | CORRECT ABSTENTION |
| 07 | Distinguishing conflict resolution from PR merging | PASS |
| 08 | Avoiding unsupported automatic-resolution guarantees | CORRECT ABSTENTION |
| 09 | Distinguishing staged and unstaged changes | PASS |
| 10 | Diagnosing repository state | PASS |

### Qualitative Summary

- Most tested answers were consistent with the available knowledge.
- The system correctly abstained on the tested questions that requested unsupported guarantees or undocumented workflow configuration.
- Test 04 exposed a partial failure when the system had to combine operational Git guidance with the distinction between resolving conflicts and completing a pull request.
- Test 07 demonstrated that the system could answer the related conceptual question when asked directly.
- Retest 04R showed that the multi-part response remained incomplete. No configuration or knowledge-base change was made as a result.

These results are qualitative findings from a small test set. They should not be interpreted as a statistically validated accuracy percentage.

---

## 6. Key Findings

### Strengths

1. Correctly identified documented Git commands in the tested scenarios.
2. Distinguished staged changes from unstaged changes.
3. Recognized when the available knowledge did not support a reliable answer.
4. Avoided unsupported guarantees about future conflict detection and automatic conflict resolution.
5. Correctly explained the difference between conflict resolution and pull-request merging when asked directly.

### Limitation Identified

The main observed limitation was incomplete handling of a multi-part question that required integrating information about local Git operations and GitHub pull-request behavior.

The relevant source information existed in the full knowledge document, but the retrieved passage did not include the clearest explanation needed for the final part of the question.

This observation does not, by itself, establish whether the primary cause was retrieval, context selection, question formulation, or answer generation.

---

## 7. Improvements and Current Status

The tests were used to identify and document the observed limitation. The retrieval configuration and knowledge documents were not changed during this evaluation.

| Finding | Action Taken | Current Status |
|---|---|---|
| Minor omission of an explicit diagnostic command in Test 02 | Recorded the need to mention `git status` for state-dependent operations | Documented improvement opportunity |
| Incomplete response to Test 04 | Inspected the actual retrieved context and reviewed the relevant pull-request source document | Investigated; not changed |
| Same limitation persisted in Test 04R | Recorded the retest result separately | Limitation remains |
| Temporary Gemini provider `503 UNAVAILABLE` error during a separate attempt | Treated as a provider availability issue rather than evidence of a retrieval failure | No retrieval change made on this evidence |

No improvement is described as completed unless a corresponding change was actually made and verified.

---

## 8. Conclusion

The ten original test cases provide evidence that Git Merge Rescue can answer common documented Git questions and appropriately acknowledge several types of knowledge limitation.

The most important finding is that the presence of relevant information in a knowledge base does not guarantee that the retrieved context will contain everything needed for a complete answer. The multi-part question and its retest exposed this limitation, while the related direct conceptual question was answered successfully.

The project therefore documents both successful behavior and an observed failure. Further work could test additional question formulations and retrieval results, but the current evaluation does not justify claiming a statistically measured accuracy rate or a verified improvement in the system.

The purpose of this evaluation is to demonstrate an evidence-based approach to testing a knowledge-grounded AI system: inspect its answers, review the retrieved context, document limitations, and make improvement decisions only when supported by evidence.
