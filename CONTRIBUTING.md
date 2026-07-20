# Contributing

<!-- Agents MUST read ./AGENTS.md. This document is for humans. -->

These contributing guidelines provide step-by-step instructions for running
an architecture audit and landing its report.

The focus here is on the mechanics and guardrails of the process. See the
[documentation](./docs/) for more general guidance on doing a good audit.

Audits may be run by anyone with write access to this repository.

See also [TS-3](https://github.com/kieranpotts/standards/tree/latest/dev/src/003)
for the technical standard that underpins this process.

> [!NOTE]
> The capitalized words REQUIRED, MUST, MUST NOT, RECOMMENDED, SHOULD,
> SHOULD NOT, OPTIONAL, and MAY herein are to be interpreted as described
> in [IETF RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).

## Workflow

1.  Decide the target codebase(s) to audit – the repositories, services, or
    filesystem directories.

2.  Branch off `main` using the convention `audit/<slug>`, where `<slug>`
    is a short, hyphen-delimited description, eg. `audit/payment-service`.

3.  Do your audit against the target codebase. See the [documentation](./docs/)
    for guidance on doing a good audit.

4.  Write up your report. Use the [template](./audits/TEMPLATE.md) as a starting
    point.

5.  Save the report at `audits/YYYY-MM-DD-<slug>/README.md`, with the metadata
    header filled in.

6.  Prepend a row to [audit index](./audits/INDEX.md).

7.  Commit your changes and open a pull request. For both the commit message
    and the PR title, use the format `audit: <description>`, where
    `<description>` is a short prose title, written full lowercase, eg.
    `audit: payment service architecture review`.

8.  Gather feedback via the normal review process.

9.  Resolve PR comments.

10. Once the review is complete, squash-merge the pull request, with the
    commit message taking the form `audit: <description>`. Delete the
    `audit/*` branch.

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

## Contributor license agreement

<!-- Delete this for closed source projects. -->

By opening a pull request to this repository, you accept and agree to the
following terms and conditions:

- You agree that your contribution may be distributed under the terms of the
  [CC0 1.0 Universal license](./LICENSE.txt), effectively releasing it to
  the public domain.

- You certify that your contribution is either created in whole by you and
  you have the right to distribute it under the designated license, or is
  based on a previous work with a compatible license that permits distribution
  and modification under the designated license.

- You understand and agree that your contribution is public and that a record
  of it, including all personal information you submit with it, is maintained
  indefinitely and may be redistributed consistent with the designated license.
