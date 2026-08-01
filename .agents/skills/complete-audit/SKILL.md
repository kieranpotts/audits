---
name: complete-audit
description: >-
  Land an audit report in the `main` trunk. Use this skill when the user
  says something like "complete this audit", "this audit is complete",
  "merge the audit", "complete the most recent audit", or
  "complete #<pr-number>".
license: CC0-1.0
metadata:
  interactive: yes
  preferred_model: ollama/prose-writing
---

# Complete audit

Land an architecture audit report in the `main` trunk.

## Parameters

Determine the following information from the surrounding context and
environment, if possible. If you're uncertain about the required parameters,
prompt the user for clarification.

- **Target — REQUIRED.** Infer the target audit report from the checked-out
  branch (`audit/<slug>`). If on `main`, try to determine the target from
  information in the context or environment. If you cannot discover the target
  for yourself, use the following command to present the user with a list of
  open pull requests, from which they can choose one to complete:

  ```sh
  gh pr list --search "audit:" --json number,title,headRefName
  ```

## Success criteria

You will achieve the following outcomes:

<!-- A merged pull request, with the source `audit/*` branch deleted from the
upstream "origin" repository. -->

- The PR is merged.

- A single new squash commit exists on `main`. The message format is
  `audit: <short lowercase description>`.

- The `audits/INDEX.md` file on `main` includes a new row for the newly-landed
  audit report.

- The `audit/*` branch no longer exists in the upstream repository.

## Instructions

1.  Verify that all feedback on the review is settled.

    ```gh
    gh api graphql -f query='
      query($owner: String!, $name: String!, $number: Int!) {
        repository(owner: $owner, name: $name) {
          pullRequest(number: $number) {
            reviewThreads(first: 100) {
              nodes { isResolved isOutdated }
            }
          }
        }
      }' -F owner=<owner> -F name=<repo> -F number=<number>
    ```

    Any `isResolved: false` node means there's outstanding feedback.

2.  Confirm the PR is not a draft.

    ```sh
    gh pr view <number> --json isDraft
    ```

    If it is still a draft, stop and direct the user to
    [`/review-audit`](../review-audit/SKILL.md) first.

3.  Confirm with the user that the PR is ready to be merged.

4.  Squash-merge the PR with the message `audit: <short lowercase description>`,
    and delete the source branch on the upstream repository:

    ```sh
    gh pr merge <number> --squash --subject "audit: <short lowercase description>" --delete-branch
    ```

5.  In case the branch was not automatically deleted from the upstream
    repository, delete it directly:

    ```sh
    git push origin --delete audit/<slug>
    ```

6.  Output a summary of your actions.

## Rules

- You MUST NOT merge a draft PR.

  Run [`/review-audit`](../review-audit/SKILL.md) first.

- You MUST NOT merge over unresolved review comments without explicit
  instruction.

- You MUST NOT merge without explicit instruction from the user.

- You MUST use the squash-merge strategy.

- You SHOULD double-check that the upstream `audit/*`  branch is deleted
  afterward.

- You MUST NOT delete the downstream `audit/*` branch. Leave that for the user
  to do, if they so choose.
