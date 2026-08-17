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

- `audits/`. One directory per audit report (`audits/YYYY-MM-DD-<slug>/`),
  dated by when the audit was performed.

  - `audits/INDEX.md` is the catalog of every audit merged into `latest/main`,
    newest first.

  - `audits/TEMPLATE.md` is the starting point for a new audit report.

- `docs/`. General guidance for humans on running and maintaining audits.

## Workflow

This is not living documentation and there is no lifecycle state machine for
audit reports.

Each audit report is a snapshot in time, true at the moment it was performed,
and immutable once merged into `latest/main`.

See [CONTRIBUTING.md > Workflow](./CONTRIBUTING.md#workflow) for the
step-by-step process for running an audit and landing its report.

It is RECOMMENDED to follow the [draft audit](./.agents/skills/draft-audit/)
skill to prepare a new report, the [review audit](./.agents/skills/review-audit/)
skill to take it out of draft, and the
[complete audit](./.agents/skills/complete-audit/) skill to land it in the
`latest/main` trunk.

## Rules

Agents MUST follow the rules in [CONTRIBUTING.md > Rules](./CONTRIBUTING.md#rules).
Re-read the rules before scoping or writing an audit report, rather than
relying on your memory of a prior state of the rules.

## Skills

The `.agents/skills/` directory provides on-demand skills for maintaining
this repository. See the [README](./.agents/skills/README.md) for descriptions
of the available skills and their triggers.

## References

The following technical standards (TS) govern this project. Fetch and ingest
the relevant standards as-and-when required for the task at hand.

- [**TS-3: Design Docs**](https://kieranpotts.com/standards/003) \
  Use when writing, reviewing, or maintaining design docs, RFCs, architecture
  decision records (ADRs), or architecture audit reports.

- [**TS-9: Version Control**](https://kieranpotts.com/standards/009) \
  Use when working with Git. Covers commits, branching, merging, integration
  strategies, cutting releases, and configuring Git/PR/CI tooling.

- [**TS-25: Technical Documentation**](https://kieranpotts.com/standards/025) \
  Use when deciding what documentation a project needs, where it should live,
  who it's for, or whether it's still trustworthy.

- [**TS-26: Technical Writing Style Guide**](https://kieranpotts.com/standards/026) \
  Use when writing or editing the prose of a technical document. Covers
  tone-of-voice, headings, terminology, lists, and citations.
