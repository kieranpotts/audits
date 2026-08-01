---
name: review-audit
description: >-
  Take an audit report's pull request out of draft once it has enough
  substance for reviewers to weigh in. Use this skill when the user says
  something like "review this audit", "this audit is ready for review",
  "take the audit out of draft", "mark the audit ready for review", or
  "review audit".
license: MIT
metadata:
  interactive: yes
  preferred_model: prose-writing
---

# Review audit

Use this skill to remove an audit report's pull request from its draft state
once there is enough substance for reviewers to weigh in. This is a light
completeness check, not a final sign-off — the findings, themes, and
priorities MAY still be refined in response to review feedback. This skill
only confirms there is something real to review.

## Parameters

Determine the following information from the surrounding context and
environment, if possible.

- **Target — REQUIRED.** Infer the target audit report from the checked-out
  branch (`audit/<slug>`). If on `main`, list open draft pull requests
  matching `audit:` and ask the user to choose:

  ```sh
  gh pr list --draft --search "audit:" --json number,title,headRefName
  ```

## Success criteria

You will achieve the following outcomes:

- The PR is no longer a draft (`isDraft: false`).

- The header metadata (auditors, audit date, scope, PR number) is filled in.

- At least one finding is documented, each naming a type, priority, and
  location.

- No literal template placeholder text remains in the header.

## Instructions

1.  Identify the audit report and its PR.

    Infer the target from the checked-out branch (`audit/<slug>`). If on
    `main`, list open draft pull requests and ask the user to choose.

2.  Do a light completeness check.

    Read `audits/YYYY-MM-DD-<slug>/README.md` in full.

    - Confirm the header fields (auditors, audit date, scope, PR) are filled
      in, not left as template placeholders (`Your Name`, `YYYY-MM-DD`,
      `owner/repo@<commit>`, `#...`).
    - Confirm at least one finding row exists in the findings table, and each
      listed finding has its own subsection with a type, priority, and
      location.

    Report any gaps to the user and stop. Do NOT block on stylistic polish,
    an empty `Themes` or `Priorities` section, or partial findings coverage —
    those are exactly what review is for.

3.  Remove the PR's draft status.

    ```sh
    gh pr ready <number>
    ```

4.  Output a summary of your actions.

## Rules

- You MUST NOT mark ready a report with no findings at all.

  A report with zero findings has nothing for a reviewer to weigh in on.

- You MUST NOT require the report to be finished.

  Themes, priorities, and additional findings MAY still be added in response
  to review feedback. This skill checks for substance, not completion.

- You MUST NOT edit the report's content yourself.

  Flag gaps to the user; do not fill them in on their behalf.

- You MUST NOT merge the pull request.

  That is [`/complete-audit`](../complete-audit/SKILL.md)'s job, once review
  is settled.
