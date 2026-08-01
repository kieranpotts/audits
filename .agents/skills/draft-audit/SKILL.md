---
name: draft-audit
description: >-
  Draft an architecture audit report. Use this skill when the user wants to
  start a new audit, or says something like "draft an audit",
  "draft a new audit report", "prepare a new audit report",
  "start an architectural review", or
  "prepare an audit of <component-or-service>".
license: CC0-1.0
metadata:
  interactive: yes
  preferred_model: ollama/prose-writing
---

# Draft audit

Scaffold a new, blank architecture audit report, ready for the user to fill in.
Do not evaluate the architecture, or help the user to write the findings into
the report.

## Parameters

Determine the following information from the surrounding context and
environment, if possible. If you're uncertain about the required parameters,
prompt the user for clarification.

- **Scope — REQUIRED.** A description of the target software system, subsystem,
  service, or other component that is the subject of the architecture audit.
  This SHOULD be scoped to a version or commit — assume the `HEAD` commit if
  you're not sure.

- **Auditors — OPTIONAL.** Assume the current team or organization are the
  auditors. Can this be discovered from the target project's `AGENTS.md` file
  or other sources?

- **Audit date — OPTIONAL.** Assume it's happening today. Use the Unix command
  `date` to determine the current date.

## Success criteria

You will achieve the following outcomes:

- Branch `audit/<slug>` exists and is checked out.

- `audits/YYYY-MM-DD-<slug>/README.md` exists. It follows the structure of
  `audits/TEMPLATE.md`. The header section is filled in as best you can.

- `audits/INDEX.md` has a new row at the top of the list.

- A draft pull request is open with the title
  `audit: <short lowercase description>`.

- The report's `Audit PR` header field names that pull request.

## Instructions

1.  From the scope, establish a short description of the audit, in the present
    tense, full lowercase, and NOT terminated by a period. Keep this in memory.

2.  Transform the description into a hyphen-delimited URL path slug. For
    example, the description "payment service" becomes the slug
    "payment-service", and "checkout api" becomes "checkout-api".

3.  Create the branch.

    ```sh
    git checkout main
    git pull --rebase
    git checkout -b audit/<slug>
    ```

4.  Copy `audits/TEMPLATE.md` to `audits/YYYY-MM-DD-<slug>/README.md`.

    YYYY-MM-DD is the current date.

5.  Fill in the headers (auditors, audit date, scope) as best you can.

    Leave the PR number — this is not yet known.

    Leave other sections as placeholders.

6.  Append a row to `audits/INDEX.md`. Add the new entry to the top of the
    table (newest first).

    Fill in the date and scope. Leave the priority findings blank or "TBC".

7.  Commit and push your changes.

    ```sh
    git add audits/YYYY-MM-DD-<slug>/README.md audits/INDEX.md
    git commit -m "audit: <short lowercase description>"
    git push -u origin audit/<slug>
    ```

8.  Open a draft pull request.

    ```sh
    gh pr create --draft --title "audit: <short lowercase description>" --fill
    ```

    If the `gh` client is unavailable or not authenticated, fail with an error.

9.  Add the new PR number to the header field in the audit report file.

    Commit and push the change.

    ```sh
    git add audits/YYYY-MM-DD-<slug>/README.md
    git commit -m "chore: add pr number to architectural audit report"
    git push -u origin audit/<slug>
    ```

10. Output a summary of your actions.

## Rules

- There MUST be exactly one new audit report per branch and per pull request.

- You MUST branch from `main`, not from any other branch. If local `main` is
  behind the remote, pull first. Use the rebase strategy to maintain a linear
  history.

- You MUST stage and commit only the files you changed, including
  `audits/INDEX.md`.

- You SHOULD record the pull request number in the report's `Audit PR` header
  field.

- You MUST NOT evaluate the architecture or write findings. This is
  out-of-scope for this skill.
