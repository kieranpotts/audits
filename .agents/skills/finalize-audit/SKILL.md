---
name: finalize-audit
description: >-
  Land an audit in the `main` trunk. Use this skill when the user says
  something like "finalize this audit", "this is finalized", "merge the audit",
  "finalize the most recent audit", or "finalize #<pr-number>".
license: MIT
metadata:
  interactive: yes
  preferred_model: prose-writing
---

# Finalize audit

Land an audit in the `main` trunk. Merge its pull request once review is settled.

**Input:** Determine the following information from the surrounding context and
environment, if possible.

- Target — REQUIRED.
  Infer the target audit report from the checked-out branch (`audit/<slug>`).
  If on `main`, try to determine the target from information in the context
  or environment. Ask the user to specify the target if you cannot discover it
  for yourself. Use the following command to present the user with a list of
  open audit pull requests, from which they can choose one to finalize:

  ```sh
  gh pr list --search "audit:" --json number,title,headRefName
  ```

**Output:** A merged pull request, with the source `audit/*` branch deleted
from the upstream "origin" repository.

## Instructions

1.  **Verify the review is settled.**

    Confirm review feedback on the pull request has been addressed.

2.  **Confirm with the user that the PR is ready to merge.**

3.  **Merge the pull request.**

    Squash-merge it with the message `audit: <short lowercase description>`:

    ```sh
    gh pr merge <number> --squash --subject "audit: <short lowercase description>"
    ```

4.  **Delete the branch.**

    Delete the source `audit/*` branch from the upstream repository, if it is
    not automatically deleted by the PR merge process.

5.  **Confirm the outcomes.**

    Output a summary of your actions.

## Rules

- **You MUST NOT merge over unresolved review comments without explicit instruction.**

- **You MUST NOT merge without explicit instruction from the user.**

- **You MUST use the squash-merge strategy.**

- **You SHOULD double-check that the upstream `audit/*`  branch is deleted afterward.**

- **You MUST NOT delete the downstream `audit/*` branch.**

## Success criteria

- **The PR is merged.**

- **A single new squash commit exists on `main`.**

  The message format is `audit: <short lowercase description>`.

- **The audit exists in the index file.**

  The `audits/INDEX.md` file on `main` includes a new row for the newly-landed
  audit report.

- **Branch `audit/<slug>` no longer exists in the upstream repository.**
