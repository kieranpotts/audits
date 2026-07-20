# [Project Name] – Audits

The capitalized words REQUIRED, MUST, MUST NOT, RECOMMENDED, SHOULD,
SHOULD NOT, OPTIONAL, and MAY are to be interpreted as described in
[IETF RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).

## Project overview

This repository holds architecture audits for [Project Name]. These are
standalone, point-in-time evaluations of the as-built system's structural health.

This is documentation, not code. There's nothing to build, lint, or run.

Audits are scoped to architecture. Security and privacy review is a separate
concern, done through threat modeling and tracked in the
[risk register](https://github.com/kieranpotts/risks).

An audit is NOT living documentation kept in sync with production. Rather, each
audit report is a snapshot in time, true at the moment it was performed, and
immutable once merged into the `main` trunk.

The [audit index](./audits/INDEX.md) is the append-only catalog of every audit
performed against the system historically.

The process of auditing the system involves reading and analyzing the source
code, and generating a report on the system's structural health. Code smells
like shallow abstractions, tangled dependencies, single-caller wrappers, leaky
boundaries, and repeated patterns are reported in a prioritized, bounded list.

Audits are evaluation only. A finding may point toward a fix, but it never
works up an alternative design.

An audit evaluates the as-built system on its own terms, without
cross-referencing the intended architecture captured in
[design docs](https://github.com/kieranpotts/design). This deliberate
blindness keeps the review unbiased, so it surfaces genuinely novel
suggestions.

## Project structure

- **`audits/`** — One directory per audit report (`audits/YYYY-MM-DD-<slug>/`),
  dated by when the audit was performed.

  - **`audits/INDEX.md`** — The catalog of every audit merged into `main`,
    newest first.

  - **`audits/TEMPLATE.md`** — The starting point for a new audit report.

- **`docs/`** — General guidance for humans on running and maintaining audits.

## Workflow

1.  An new audit report is introduced via an `audit/<slug>` branch. It is
    RECOMMENDED that agents follow the
    [scaffold audit](./.agents/skills/scaffold-audit/) skill to help
    prepare a new audit report in a new branch, ready for the user to
    complete the report.

2.  The user undertakes the architecture audit and writes up the report.

3.  The user opens a pull request and invites peers to review the report.

4.  Once the review is complete, the audit report is squash-merged into the
    `main` trunk and the PR is closed. It is RECOMMENDED that agents follow
    [finalize audit](./.agents/skills/finalize-audit/) skill if the user
    requests help completing this step.

## Rules

- Audit reports MUST be written in American English.

- Every report MUST be dated.

- Every audit report MUST be expressly scoped to either the whole system or a
  specific part of it.

- If possible, the exact revision of the software that's audited SHOULD be
  specified, eg. `<team>/<repo>@<commit-hash>`.

- An audit report MUST be scoped exclusively to the as-built static structure of
  the system's code and data. Security and privacy findings – eg. injection points,
  broken auth boundaries, unsafe secrets handling — are out-of-scope; these
  concerns belong in the [risk register](https://github.com/kieranpotts/risks).
  Also out-of-scope is catching drift from the intended architecture; design
  docs SHOULD NOT be reviewed as part of an architectural audit, only the
  source code of the system itself.

- Every finding MUST cite specific files and lines. Vague findings (eg. "the
  API layer is messy") are not acceptable — such findings cannot be easily
  actioned.

- Once merged, an audit report MUST NOT be further edited. Audit reports on
  `main` MUST be treated as immutable, since they are snapshots in time, not
  living documentation. Reassessments of the architecture are done by adding
  new audit reports, not by amending previous ones.

- Architecture audits are evaluation only. Reports SHOULD NOT suggest fixes
  or alternative designs, only report on possible cruft. No code should be
  changed, or pull requests opened against code repositories, as part of
  an architectural audit. That happens downstream as an outcome of the audit.

- The GitHub issue tracker SHOULD be used only for maintenance work on this
  repository itself. Issues SHOULD NOT be used as part of the audit report
  workflow.

## Skills

Skills to help agents maintain this repository are included in the
[`.agents/skills/`](./.agents/skills/) directory.
