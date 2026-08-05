---
name: review-audit
description: >-
  Take an audit report's pull request out of draft once it has enough
  substance for reviewers to weigh in. Use this skill when the user says
  something like "review this audit", "this audit is ready for review",
  "take the audit out of draft", "mark the audit ready for review", or
  "review audit".
compatibility: requires Read, Bash (git/gh)
license: CC0-1.0
---

# Review audit

Check an audit report has enough substance for review, and take its pull
request out of draft.

## Parameters

Determine the following information from the surrounding context and
environment, if possible. If you're uncertain about the required parameters,
prompt the user for clarification.

- **Target — REQUIRED.** Infer the target audit report from the checked-out
  branch (`audit/<slug>`). If on `main`, list open draft pull requests
  matching `audit:` and ask the user to choose one.

  ```sh
  gh pr list --draft --search "audit:" --json number,title,headRefName
  ```

## Success criteria

- The PR MUST no longer be a draft (`isDraft: false`).

- The header metadata (auditors, audit date, scope, PR number) MUST be filled in.

- At least one finding MUST be documented.

- Each finding MUST have a type, priority, and location.

- The audit report MUST NOT contain any literal template placeholder text.

## Instructions

1.  Check the audit report for completeness. It has to be sufficiently complete
    to invite feedback from the team.

    Read `audits/YYYY-MM-DD-<slug>/README.md` in full.

    - Confirm the header fields (auditors, audit date, scope, PR) are filled
      in. There MUST NOT be any placeholder text left in the headers — compare
      against the template, `audits/TEMPLATE.md`

    - Confirm at least one finding row exists in the findings table.

    - Each finding MUST have its own subsection with a type, priority, and
      location.

    Report any gaps to the user and stop.

2.  Remove the PR's draft status.

    ```sh
    gh pr ready <number>
    ```

3.  Output a summary of your actions.

## Rules

- You MUST NOT mark as "ready for review" a report that has no findings at all.

- You MUST NOT require the report to be fully finished. It is okay for sections
  like "themes" and "priorities" to be incomplete, insubstantial, or missing
  entirely.

- You MUST NOT edit the report's content yourself.

- You MUST NOT merge the pull request.
