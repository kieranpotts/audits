---
name: scaffold-audit
description: >-
  Scaffold an architecture audit. Use this skill when the user wants to start a
  new audit, or says something like "scaffold an audit", "draft a new audit
  report", "prepare a new audit report", "start an architectural review", or
  "prepare an audit of <component or service name>".
license: MIT
metadata:
  interactive: yes
  preferred_model: prose-writing
---

# Scaffold audit

Scaffold an architecture audit. Create the branch, ask a few questions to
fill out the report headers and initial sections, and open a draft PR.

Do not evaluate the architecture or help the user to write the findings.

**Input:** Determine the following information from the surrounding context and
environment, if possible. If you're uncertain about the input requirements,
prompt the user for clarification.

- Scope — REQUIRED.
  A description of the target software system, subsystem, servic, or other
  component that is the subject of the architectural review. Preferably
  scoped to a specific version, release, commit, or other revision.

- Auditors — OPTIONAL.
  Assume the current team or organization as the auditors. Can this be
  discovered from the target project's `AGENTS.md` file or other sources?

- Audit date — OPTIONAL.
  Assume it's happening today. Use the Unix command `date` to determine the
  current date.

**Output:** You will write a new file to `audits/YYYY-MM-DD-<slug>/README.md`,
based on the template at `audits/TEMPLATE.md`, committed to a branch named
`audit/<slug>`, pushed to the upstream "origin" repository, and a draft pull
request opened with `main` as the target branch.

## Instructions

1.  **Determine the description and slug.**

    From the scope of the audit, establish a short description of it, written
    in present tense, full lowercase, and NOT terminated by a period.

    From the description, establish a hyphen-delimited URL path slug. For
    example, the description "payment service" becomes the slug "payment-service",
    and "checkout api" becomes "checkout-api".

2.  **Create the branch.**

    ```sh
    git checkout main
    git pull --rebase
    git checkout -b audit/<slug>
    ```

3.  **Copy the template.**

    Copy [`audits/TEMPLATE.md`](../../../audits/TEMPLATE.md) to
    `audits/YYYY-MM-DD-<slug>/README.md`.

    YYYY-MM-DD is the current date.

4.  **Fill in the headers.**

    Fill in the headers (auditors, audit date, scope).

    Leave the PR number — this is not yet known.

    Leave the summary, scope and method, findings, themes, and priorities
    sections as placeholders.

5.  **Add to the index.**

    Append a row to [`audits/INDEX.md`](../../../audits/INDEX.md). Add the new
    entry to the top of the table (newest first).

    Fill in the date and scope. Leave the priority findings blank or "TBD".

6.  **Commit and push your changes.**

    ```sh
    git add audits/YYYY-MM-DD-<slug>/README.md
    git commit -m "audit: <description>"
    git push -u origin audit/<slug>
    ```

    The `<description>` MUST be written full lowercase with no period,
    eg. "payment service". Do NOT use the slug form here.

7.  **Open a draft pull request.**

    ```sh
    gh pr create --draft --title "audit: <description>" --fill
    ```

    If the `gh` client is not authenticated, fail with an error.

8.  **Update the PR number.**

    Add the new PR number to the header field in the audit report file.

    Commit and push the change.

    ```sh
    git add audits/YYYY-MM-DD-<slug>/README.md
    git commit -m "chore: add pr reference number"
    git push -u origin audit/<slug>
    ```

9.  **Confirm the outcomes.**

    Output a summary of your actions.

## Rules

- **There MUST be exactly one new audit report per branch and per pull request.**

  Do not bundle multiple target codebases into one PR. Scaffold a separate
  audit for each.

- **You MUST branch from `main`, not from any other branch.**

  Audits are always cut from `main`. If local `main` is behind the remote,
  pull first. Use the rebase strategy to maintain a linear history on the
  `main` trunk.

- **You MUST NOT evaluate the architecture or write findings.**

  This skill only scaffolds the report and its PR. Evaluating the target
  codebase and writing up the findings, themes, and priorities is out-of-scope.

## Success criteria

- **Branch `audit/<slug>` exists and is checked out.**

- **`audits/YYYY-MM-DD-<slug>/README.md` exists.**

  It follows the [`TEMPLATE.md`](../../../audits/TEMPLATE.md) structure,
  with the header section filled in.

- **`audits/INDEX.md` has a new row.**

  The new entry is appended to the top of the list.

- **A draft pull request is open.**

  The title of the PR is `audit: <short lowercase description>`.

  The PR is in the draft state, which means it's not yet ready for review.
