# Contributing

<!-- Agents MUST read ./AGENTS.md. This document is for humans. -->

These contributing guidelines provide step-by-step instructions for running
an audit and landing its report. The focus here is on the mechanics and
guardrails of the process. See the [documentation](./docs/) for more general
guidance on doing a good audit.

Audits may be run by anyone with write access to this repository.

> [!NOTE]
> The capitalized words REQUIRED, MUST, MUST NOT, RECOMMENDED, SHOULD,
> SHOULD NOT, OPTIONAL, and MAY herein are to be interpreted as described
> in [IETF RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).

## Overview

An audit is a standalone, point-in-time evaluation of [Project Name]'s
as-built architecture. Security and privacy review is a separate concern,
tracked in the [risk register](https://github.com/kieranpotts/risks).

Unlike the sibling [design docs](https://github.com/kieranpotts/design)
repository, an audit is not living documentation. Each audit report is a
snapshot, true at the moment it was performed, and immutable once merged into
the `main` trunk. By comparison, design docs evolve in lock-step with the
production system.

## The audit workflow

Unlike a design change, an audit has no lifecycle state machine. It is
scoped, performed, and merged in a single pass.

### Step 1: Scope the audit

Decide the target codebase(s) to audit – which repositories, services, or
filesystem directories.

### Step 2: Open a pull request

1.  Branch off `main` using the convention `audit/<slug>`, where `<slug>`
    is a short, hyphen-delimited description, eg. `audit/payment-service`.

2.  Do your audit against the target codebase. See the [documentation](./docs/)
    for guidance on doing a good audit.

3.  Write up your report. Use [`TEMPLATE.md`](./audits/TEMPLATE.md) as a basis.
    Save the report at `audits/YYYY-MM-DD-<slug>/README.md`, with the metadata
    header filled in – Auditors, Date, Scope (`owner/repo@commit`).

4.  Prepend a row to [`audits/INDEX.md`](./audits/INDEX.md),
    in the same commit.

5.  Commit your changes and open a pull request titled `audit: <description>`,
    where `<description>` is a short prose title, written full lowercase,
    eg. `audit: payment service architecture review`.

### Step 3: Review

Gather feedback via normal pull request comments. No discussion thread is
required. An audit is a set of findings to review, not a decision to debate.

### Step 4: Merge

Once review is settled, squash-merge the pull request, with a message of
the form `audit: <description>`. Delete the branch.

## Rules

- Audit reports MUST be written in American English.

- Every report MUST be dated, scoped, and cite the exact `repo@commit` examined.

- Every finding MUST cite specific files and lines, state what is observed and
  the cost it imposes, before optionally pointing toward a fix – never a
  worked-out alternative design.

- An audit MUST NOT read the design documentation, and MUST NOT report
  drift from it.

- An audit MUST NOT change any code, file issues, or open pull requests
  against the audited repositories.

- Once merged, a report is immutable. To reassess a system, open a new audit.

- The GitHub issue tracker is used only for maintenance work on this repository
  itself.

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
