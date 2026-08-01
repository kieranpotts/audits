# [Project Name] – Architecture Audits

The capitalized words REQUIRED, MUST, MUST NOT, RECOMMENDED, SHOULD,
SHOULD NOT, OPTIONAL, and MAY are to be interpreted as described in
[IETF RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).

## Project overview

See the [README](./README.md) for an overview of this project, and how it fits
alongside the sibling SRS, RFC, design, plans, and risks repositories.

This repository is documentation, not code. There is nothing to build, lint,
or run.

## Project structure

- **`audits/`:** One directory per audit report (`audits/YYYY-MM-DD-<slug>/`),
  dated by when the audit was performed.

  - **`audits/INDEX.md`** is the catalog of every audit merged into `main`,
    newest first.

  - **`audits/TEMPLATE.md`** is the starting point for a new audit report.

- **`docs/`:** General guidance for humans on running and maintaining audits.

## Workflow

This is not living documentation and there is no lifecycle state machine for
audit reports.

Each audit report is a snapshot in time, true at the moment it was performed,
and immutable once merged into `main`.

See [CONTRIBUTING.md > Workflow](./CONTRIBUTING.md#workflow) for the
step-by-step process for running an audit and landing its report.

It is RECOMMENDED to follow the [draft audit](./.agents/skills/draft-audit/)
skill to prepare a new report, the [review audit](./.agents/skills/review-audit/)
skill to take it out of draft, and the
[complete audit](./.agents/skills/complete-audit/) skill to land it in the
`main` trunk.

## Rules

Agents MUST follow the rules in [CONTRIBUTING.md > Rules](./CONTRIBUTING.md#rules).
Re-read the rules before scoping or writing an audit report, rather than
relying on your memory of a prior state of the rules.

## Skills

The **`.agents/skills/`** directory provides on-demand skills for maintaining
this repository. See the [README](./.agents/skills/README.md) for descriptions
of the available skills and their triggers.
