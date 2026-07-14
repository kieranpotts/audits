---
name: finalize-audit
description: >-
  Land an audit in the `main` trunk. Merge its pull request once review is
  settled. Use when the user says "finalize this audit", "merge the audit",
  "the audit is finalized", or "land the audit PR".
license: MIT
metadata:
  interactive: yes
  preferred_model: prose-writing
---

# Finalize audit

**Input**: The agent requires knowledge of the target architectural audit
that is now final. The agent may prompt the user to specify the target audit
report, if not obvious from the context.

**Output**: The agent merges the pull request and deletes the `audit/*` branch.
The agent confirms the outcome.

##  Instructions

1.  **Identify the audit.**

    Infer the target from the checked-out branch (`audit/<slug>`). If on
    `main`, use the user's description, or list open audit pull requests and
    ask the user to choose:

    ```sh
    gh pr list --search "audit:" --json number,title,headRefName
    ```

2.  **Verify the review is settled.**

    Confirm review feedback on the pull request has been addressed. Do not
    merge over unresolved comments without the user's explicit instruction.

3.  **Merge the pull request.**

    Confirm with the user that the PR is ready to merge. Do not merge without
    explicit instruction.

    Once confirmed, squash-merge it with an `audit: <short lowercase description>`
    message:

    ```sh
    gh pr merge <number> --squash --subject "audit: <short lowercase description>"
    ```

4.  **Delete the branch.**

    Delete the source `audit/*` branch from the upstream repository, if it is
    not automatically deleted.

5.  **Confirm the outcomes.**

    Output a summary of your actions.

##  Rules

-   **Never merge over unresolved review comments without explicit instruction.**

-   **Do not merge without explicit instruction from the user.**

-   **Use the squash-merge strategy.**

    Use the format `audit: <short lowercase description>` for the squash-commit
    message.

##  Success criteria

-   **The PR is merged.**

-   **A new squash commit exists on `main`.**

    The message format is `audit: <short lowercase description>`.

-   **The audit exists in the index file.**

    The `audits/INDEX.md` file on `main` includes the new audit's row.

-   **Branch `audit/<slug>` no longer exists in the upstream repository.**
