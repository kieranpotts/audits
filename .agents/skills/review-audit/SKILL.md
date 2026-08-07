---
name: review-audit
description: >-
  Check that an architecture audit report has enough substance for reviewers
  to weigh in on, then take its pull request out of draft. Use when the user
  says something like "review this audit", "this audit is ready for review",
  "take the audit out of draft", "mark the audit ready for review", or
  "review audit". Do not use it to fill gaps in the report, or to merge the
  pull request.
compatibility: >-
  requires Read, Glob, Bash (git, gh)
license: CC0-1.0
---

# Review audit

Check that an audit report has enough substance for reviewers, and take its
pull request out of draft. Do not write or edit the report's content yourself,
and do not merge.

## Parameters

Determine the following information from the surrounding context and
environment, if possible. If you're uncertain about the required parameters,
prompt the user for clarification.

- **Target — REQUIRED.** The audit report to check. Infer it from the
  checked-out branch, which follows the pattern `audit/<slug>`; the report is
  then the sole `audits/YYYY-MM-DD-<slug>/README.md` on that branch. If `main`
  is checked out, list the open draft pull requests and ask the user to pick
  one.

  ```sh
  gh pr list --draft --search "audit:" --json number,title,headRefName
  ```

## Success criteria

- The pull request MUST no longer be a draft, verifiable as `isDraft: false`
  from `gh pr view <number> --json isDraft`.

- The report's header fields — auditors, audit date, audit PR, scope — MUST
  all be filled in, and no template placeholder text MUST remain anywhere in
  the report.

- The findings table MUST list at least one finding, and every listed finding
  MUST have its own subsection giving a type, a priority, and a location.

- The report's content MUST be byte-for-byte unchanged: this skill reads and
  reports, it never repairs.

- The pull request MUST still be open and unmerged.

## Instructions

1.  Read `audits/YYYY-MM-DD-<slug>/README.md` in full, and read
    `audits/TEMPLATE.md` alongside it so you can recognize placeholder text
    that has been left in place.

2.  Check the report against the success criteria above: header fields
    complete, at least one finding in the table, each finding written up with
    a type, a priority, and a location, and no placeholder prose left over.

    If any check fails, report every gap you found to the user and stop. Do
    not take the pull request out of draft, and do not fix the gaps yourself.

3.  Remove the pull request's draft status.

    ```sh
    gh pr ready <number>
    ```

4.  Summarize what you did: the report checked, any weaknesses you noticed but
    did not treat as blocking, and the pull request now awaiting review.

## Rules

- You MUST NOT mark a report ready for review when it documents no findings
  at all. There is nothing for a reviewer to respond to.

- You MUST NOT hold the report to a standard of completeness. Sections such as
  "themes" and "priorities" MAY be thin, or missing entirely — those are
  usually written in response to review feedback, so demanding them up front
  inverts the workflow.

- You MUST NOT edit the report's content, or the audit index, yourself.
  Reporting a gap and letting the user close it keeps authorship of the audit
  with the auditor.

- You MUST NOT merge the pull request.

## Edge cases

- The branch holds more than one audit report directory.

  Each branch is meant to carry exactly one report. Stop, name the report
  directories you found, and ask the user which one to check.

- The pull request is already out of draft.

  Run the completeness checks anyway and report the outcome, but treat the
  `gh pr ready` step as already satisfied rather than an error.
