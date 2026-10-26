---
name: pull-request-code-review
description: "Review a GitHub pull request or a GitLab merge request for correctness, missing tests, and security issues in the diff. Use when the user asks for a pull request review, a merge request review, or a review of a branch before merge."
user-invocable: true
license: Apache-2.0
compatibility: Designed for Claude Code, Cursor, and similar AI coding agents. Requires git. GitHub reviews use gh. GitLab reviews use glab.
metadata:
  author: zhongshixi
  version: "0.0.1"
  category: engineering
allowed-tools: Read Edit Write Glob Grep Bash(git:*) Bash(gh:*) Bash(glab:*) Agent
---

# Review Steps

## 1. Confirm the reviewer

If the user is not an assigned reviewer, ask whether to continue. Review only an open pull request or merge request.

## 2. Prepare the review

1. On GitHub, use `gh pr diff` and `gh pr view` when the pull request number is known. On GitLab, use `glab mr diff` and `glab mr view` when the merge request number is known.
2. The working directory must be the target repository. If it is not, ask the user to clone it.
3. Update the local base branch and head branch.
4. Skip the review when this skill already reviewed the current head commit. Review again when that commit has changed.
5. Read changed files and the code they call or that calls them. Leave the rest of the repository unread.
6. Do not modify code.
7. Do not open credential or secret files.

## 3. Verify the changed behavior

When the pull request or merge request states its intent, find where the change misses that intent: a stated case left unhandled, or behavior that contradicts the intent. Trace the new path for wrong results, dropped errors, and broken callers. Follow a call outside the diff when the diff can trigger a bug there.

## 4. Classify review effort

### High-risk items

Crashes, exceptions, memory leaks, races, deadlocks, cache corruption, missing retries, missing authentication or permissions, breaking changes to contracts other modules depend on, and code that does not build.

### Medium-risk items

Mistakes in feature or bug-fix logic.

### Low-risk items

Mechanical changes: renames, formatting, documentation, comments, version bumps, test-only changes, generated code, config values with no logic, and indentation. Treat indentation as high-risk in languages where indentation is syntax, such as Python.

## 5. Check the tests

Point to a test that fails when the change is reverted, or report the missing test.

## 6. Write the review comment

Post the comment as the authenticated GitHub or GitLab user. For each finding:

1. risk-level: high, medium, or low
2. description: the issue and its category
3. reason: why it is an issue, and the scenario that triggers it
4. suggestion: one or more fixes

End the comment with the name of the model that produced the review.

## 7. Approve the Pull Request
If all high-risk items and medium-risk items are not found or they are addressed by follow-up commits, approve the pull request