---
name: complete-audit
description: >-
  Land an architecture audit report in the `latest/main` trunk by squash-merging its
  pull request and deleting the audit branch. Use when the user says something
  like "complete this audit", "this audit is complete", "merge the audit",
  "complete the most recent audit", or "complete #<pr-number>". Do not use it
  to take a pull request out of draft, or to edit the report.
compatibility: >-
  requires Read, Bash (git, gh)
license: CC0-1.0
---

# Complete audit

Check that an audit report is settled, then squash-merge it into the
`latest/main` trunk and delete its branch upstream. Do not edit the report on
the way through, and do not merge without the user's say-so.

## Parameters

Determine the following information from the surrounding context and
environment, if possible. If you're uncertain about the required parameters,
prompt the user for clarification.

- **Target — REQUIRED.** The audit report to land. Infer it from the
  checked-out branch, which follows the pattern `latest/audit/<slug>`. If
  `latest/main` is checked out, list the open non-draft pull requests and ask
  the user to pick one.

  ```sh
  gh pr list --search "create:" --json number,title,headRefName
  ```

## Success criteria

- The pull request MUST be merged.

- A single new squash commit MUST exist on `latest/main`, its message taking the
  form `update: <short lowercase description>`.

- `audits/INDEX.md` on `latest/main` MUST carry a row for the newly-landed report,
  pointing at its directory.

- The `latest/audit/<slug>` branch MUST no longer exist in the upstream repository.

- The merge MUST have introduced no changes to the report's content. Reports
  are immutable snapshots, so landing one is a pure transport step.

## Instructions

1.  Confirm the pull request is not still a draft.

    ```sh
    gh pr view <number> --json isDraft
    ```

    If it is a draft, stop and tell the user it has to be marked ready for
    review first.

2.  Confirm that all review feedback is settled.

    ```sh
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

    Any node with `isResolved: false` is outstanding feedback. Stop and warn
    the user.

3.  Confirm the report itself is landable: its header fields are filled in,
    and `audits/INDEX.md` on the branch already carries its row. A missing
    index row is the common defect, because the row is written at drafting
    time and is easy to lose in a rebase. Report either gap and stop.

4.  Ask the user to confirm the merge. You MUST NOT proceed past this step
    without their explicit go-ahead, because a merged report is immutable and
    cannot be corrected in place afterward.

5.  Squash-merge, and delete the source branch upstream.

    ```sh
    gh pr merge <number> --squash \
      --subject "update: <short lowercase description>" --delete-branch
    ```

6.  If the branch survived the merge, delete it upstream directly.

    ```sh
    git push origin --delete latest/audit/<slug>
    ```

7.  Summarize what you did: the report landed, the squash commit, and the
    state of the upstream branch.

## Rules

- You MUST NOT merge a pull request that is still a draft.

- You MUST NOT merge over unresolved review threads unless the user explicitly
  instructs you to.

- You MUST use the squash-merge strategy, so each audit report lands as
  exactly one commit on `latest/main`.

- You MUST NOT edit the report's content, or the audit index, as part of
  landing it. Once a report is on `latest/main` it is immutable; a reassessment
  is a new report, never an amendment to an old one.

- You SHOULD NOT delete the local `latest/audit/<slug>` branch. Leave that
  cleanup to the user, who may still want the working copy.

## Edge cases

- The merge is blocked by a merge conflict against `latest/main`.

  Stop and report it. Rebasing an audit branch touches the index file that
  both sides changed, and the resolution is the user's call, not yours.
