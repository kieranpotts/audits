---
name: draft-audit
description: >-
  Scaffold the branch, report file, index row, and draft pull request for a
  new architecture audit. Use when the user wants to start a new audit, or
  says something like "draft an audit", "draft a new audit report", "prepare
  a new audit report", "start an architectural review", or "prepare an audit
  of <component-or-service>". Do not use it to evaluate the architecture or
  to write the findings.
compatibility: >-
  requires Read, Write, Edit, Bash (git, gh, date)
license: CC0-1.0
---

# Draft audit

Scaffold a new, blank architecture audit report, ready for the user to fill in.
Do not evaluate the architecture, and do not help the user write findings into
the report.

## Parameters

Determine the following information from the surrounding context and
environment, if possible. If you're uncertain about the required parameters,
prompt the user for clarification.

- **Scope — REQUIRED.** A description of the target software system,
  subsystem, service, or other component under audit. This SHOULD be pinned to
  a version or commit, in the form `owner/repo@<commit>`. Assume the target's
  `HEAD` commit if you cannot determine one.

- **Auditors — OPTIONAL.** Assume the current team or organization are the
  auditors. Try to discover names and handles from the target project's
  `AGENTS.md`, `README.md`, or Git history before asking.

- **Audit date — OPTIONAL.** Assume the audit is happening today. Read the
  current date from the `date` command rather than from your own assumptions,
  which may be stale.

## Success criteria

- Branch `audit/<slug>` MUST exist and be checked out.

- `audits/YYYY-MM-DD-<slug>/README.md` MUST exist, and MUST follow the
  structure of `audits/TEMPLATE.md`.

- The report's header fields — auditors, audit date, audit PR, scope — MUST
  all be filled in, with no template placeholder text left behind.

- `audits/INDEX.md` MUST carry a new row for this audit at the top of the
  table.

- A pull request MUST be open, in draft state, titled
  `create: <short lowercase description>`.

- The report's body sections MUST still hold the template's placeholder prose.
  Scaffolding an audit produces an empty report; findings are the user's work,
  written later.

- Files outside `audits/YYYY-MM-DD-<slug>/` and `audits/INDEX.md` MUST be
  unchanged, and the audited codebase MUST NOT have been modified at all.

## Instructions

1.  From the scope, compose a short description of the audit: present tense,
    full lowercase, not terminated by a period. Reuse it verbatim for the
    commit message and the pull request title, so the two match.

2.  Transform that description into a hyphen-delimited URL path slug. For
    example, "payment service" becomes `payment-service`, and "checkout api"
    becomes `checkout-api`.

3.  Cut the branch from `main`.

    ```sh
    git checkout main
    git pull --rebase
    git checkout -b audit/<slug>
    ```

4.  Copy `audits/TEMPLATE.md` to `audits/YYYY-MM-DD-<slug>/README.md`, where
    `YYYY-MM-DD` is the audit date.

5.  Fill in the report's header fields — auditors, audit date, scope. Leave
    the audit PR field as a placeholder for now; the number is not yet known.
    Leave every other section exactly as the template wrote it.

6.  Prepend a row to the table in `audits/INDEX.md`, so the newest audit sits
    at the top. Fill in the date and scope, and set the priority findings
    column to "TBC".

7.  Commit and push.

    ```sh
    git add audits/YYYY-MM-DD-<slug>/README.md audits/INDEX.md
    git commit -m "create: <short lowercase description>"
    git push -u origin audit/<slug>
    ```

8.  Open the pull request in draft state.

    ```sh
    gh pr create --draft --title "create: <short lowercase description>" --fill
    ```

    If the `gh` client is unavailable or not authenticated, stop and report
    the failure. Do not fall back to opening the pull request by other means.

9.  Write the new pull request number into the report's audit PR header field,
    then commit and push again.

    ```sh
    git add audits/YYYY-MM-DD-<slug>/README.md
    git commit -m "chore: add pr number to architecture audit report"
    git push
    ```

10. Summarize what you did: the branch, the report path, the index row, and
    the pull request number.

## Rules

- Each branch and pull request MUST carry exactly one new audit report.

  Audits are dated snapshots, indexed one row apiece. Bundling two into one
  pull request makes them impossible to land, cite, or supersede separately.

- You MUST branch from `main`, never from another audit branch, and you MUST
  pull with `--rebase` so history stays linear.

- You MUST stage only the report file and `audits/INDEX.md`. Leave any
  unrelated working-tree changes uncommitted.

- You MUST NOT evaluate the architecture or write findings into the report.
  This skill scaffolds; the audit itself happens afterward.

- You MUST NOT modify the codebase under audit. An architecture audit is
  evaluation only, and this skill does not even reach the evaluation stage.
