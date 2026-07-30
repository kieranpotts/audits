---
name: complete-audit
description: >-
  Land an audit in the `main` trunk. Use this skill when the user says
  something like "complete this audit", "this is completed", "merge the audit",
  "complete the most recent audit", or "complete #<pr-number>".
license: MIT
metadata:
  interactive: yes
  preferred_model: prose-writing
---

# Complete audit

Land an audit in the `main` trunk. Merge its pull request once review is settled.

## Input

Determine the following information from the surrounding context and environment,
if possible.

- Target — REQUIRED. Infer the target audit report from the checked-out branch
  (`audit/<slug>`). If on `main`, try to determine the target from information
  in the context or environment. Ask the user to specify the target if you
  cannot discover it for yourself. Use the following command to present the
  user with a list of open audit pull requests, from which they can choose one
  to complete:

  ```sh
  gh pr list --search "audit:" --json number,title,headRefName
  ```

## Output

A merged pull request, with the source `audit/*` branch deleted from the
upstream "origin" repository.

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

2.  Confirm with the user that the PR is ready to be merged.

3.  Squash-merge the PR with the message `audit: <short lowercase description>`,
    and delete the source branch on the upstream repository:

    ```sh
    gh pr merge <number> --squash --subject "audit: <short lowercase description>" --delete-branch
    ```

4.  In case the branch was not automatically deleted from the upstream
    repository, delete it directly:

    ```sh
    git push origin --delete audit/<slug>
    ```

5.  Output a summary of your actions.

## Rules

- You MUST NOT merge over unresolved review comments without explicit
  instruction.

- You MUST NOT merge without explicit instruction from the user.

- You MUST use the squash-merge strategy.

- You SHOULD double-check that the upstream `audit/*`  branch is deleted
  afterward.

- You MUST NOT delete the downstream `audit/*` branch. Leave that for the user
  to do, if they so choose.

## Success criteria

- The PR is merged.

- A single new squash commit exists on `main`. The message format is
  `audit: <short lowercase description>`.

- The `audits/INDEX.md` file on `main` includes a new row for the newly-landed
  audit report.

- The `audit/*` branch no longer exists in the upstream repository.

## References

- [`AGENTS.md`](../../../AGENTS.md): The full audit workflow and rules.
