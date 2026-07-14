---
name: scaffold-audit
description: >-
  Scaffold an architecture audit. Create the branch, ask a few questions to
  fill out the report headers and initial sections, and open a draft PR.
  Do not evaluate the architecture or help the user to write the findings. Use
  this skill when the user wants to start a new audit, or says "scaffold an
  audit", "draft an audit", or "start an architectural audit".
license: MIT
metadata:
  interactive: yes
  preferred_model: prose-writing
---

# Scaffold audit

**Input**: The agent requires a description of the target software system,
subsystem, services, or other component that is the subject of the
architectural review. The agent may prompt the user for this information
if not obvious from the context. The agent may also ask the user questions to
help it fill out the front-matter in the audit report.

**Output**: The agent writes a new file to `audits/YYYY-MM-DD-<slug>/README.md`,
commits it to an `audit/<slug>` branches, pushes is to the upstream origin
repository, and opens a draft pull request. The agent confirms the outcome.

##  Instructions

1.  **Determine the target.**

    Ask the user which codebase or component to audit (a path or `owner/repo`)
    if not already stated in this skill's invocation or obvious from the wider
    context.

2.  **Determine the slug and description.**

    Establish a short, hyphen-delimited slug that names the target, eg.
    `payment-service` or `checkout-api`. Decide a short prose description from
    the user's request.

3.  **Create the branch.**

    ```sh
    git checkout main
    git pull
    git checkout -b audit/<slug>
    ```

4.  **Scaffold the report.**

    Copy [`audits/TEMPLATE.md`](../../../audits/TEMPLATE.md) to
    `audits/YYYY-MM-DD-<slug>/README.md`.

    YYYY-MM-DD is the current date.

    Ask the user any questions needed to fill out the headers (auditors,
    audit date, scope) and any initial sections you can complete without
    performing the audit itself.

    Leave the findings, themes, and recommendations sections as placeholders.

5.  **Add to the index.**

    Append a row to [`audits/INDEX.md`](../../../audits/INDEX.md) — at the top
    (newest first).

    Fill in the date and scope. Leave the priority findings count blank or "TBD".

6.  **Commit and push your changes.**

    ```sh
    git add audits/
    git commit -m "audit: <short lowercase description>"
    git push -u origin audit/<slug>
    ```

7.  **Open a draft pull request.**

    ```sh
    gh pr create --draft --title "audit: <short lowercase description>" --fill
    ```

8.  **Confirm the outcomes.**

    Output a summary of your actions.

##  Rules

-   **One audit per branch and pull request.**

    Do not bundle multiple target codebases into one PR. Scaffold a separate
    audit for each.

-   **Branch from `main`, not from any other branch.**

    Audits are always cut from `main`. If local `main` is behind the remote,
    pull first.

-   **Do not evaluate the architecture or write findings.**

    This skill only scaffolds the report and its PR. Evaluating the target
    codebase and writing the findings, themes, and recommendations sections
    is a separate step.

##  Success criteria

-   **Branch `audit/<slug>` exists and is checked out.**

-   **`audits/YYYY-MM-DD-<slug>/README.md` exists.**

    It follows the [`TEMPLATE.md`](../../../audits/TEMPLATE.md) structure,
    with headers and initial sections filled out.

-   **`audits/INDEX.md` has a new row.**

    The entry for this new audit is appended to the top of the list.

-   **A draft pull request is open.**

    The title of the PR is `audit: <short lowercase description>`.

    The PR is in the draft state, which means it's not yet ready for review.
