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

An audit is NOT living documentation kept in sync with production. Each audit
report is a snapshot, true at the moment it was performed, immutable once
merged into the main trunk. The [audit index](./audits/INDEX.md) is the
append-only catalog of every audit performed on the system historically.

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

- **`audits/`**:
  One directory per audit report (`audits/YYYY-MM-DD-<slug>/`), dated by
  when the audit was performed.

  - **`audits/INDEX.md`** is the catalog of every audit merged into `main`,
    newest first.

  - **`audits/TEMPLATE.md`** is the starting point for a new audit report.

- **`docs/`**:
  General guidance for humans on running and maintaining audits.

## How an audit is introduced

Unlike a design change, an audit has no lifecycle state machine. An audit is
scoped, performed, and merged in one pass.

1. An audit is opened as a pull request on an `audit/<slug>` branch,
   scaffolded by the [scaffold audit](./.agents/skills/scaffold-audit/) skill.

2. The report is reviewed via normal pull request comments. No discussion
   thread is required. An audit is a finding to review, not a decision to
   debate.

3. Once review is settled, the [finalize audit](./.agents/skills/finalize-audit/)
   skill can be used to squash-merge the pull request and update the index.

## Rules

- Write in American English.

- Every audit report MUST be dated, scoped, and cite the exact `repo@commit`
  examined, so it is a reproducible point-in-time snapshot.

- An audit is scoped to architecture. It MUST NOT report security or privacy
  findings – injection points, broken auth boundaries, unsafe secrets handling,
  and the like. Those belong in the
  [risk register](https://github.com/kieranpotts/risks).

- Every finding MUST cite specific files and lines. Vague findings ("the
  API layer is messy") are not acceptable.

- A finding MUST state what is observed and the cost it imposes before
  offering any suggestion. A pointer toward a fix is OPTIONAL and MUST stay
  a pointer, never a worked-out alternative design.

- An audit evaluates the as-built system on its own terms. It MUST NOT read
  the design documentation, and MUST NOT report drift from it.

- An audit MUST NOT change any code, file issues, or open pull requests
  against the audited repositories. Discovery only.

- Once merged, an audit report is immutable. To reassess a system, run a
  new audit – never edit a merged one.

- The GitHub issue tracker is used only for maintenance work on this
  repository itself (via the `MAINTENANCE` template).

## Skills

The [`.agents/skills/`](./.agents/skills/) directory is reserved for
on-demand skills that help run and maintain the audit workflow. See the
[README](./.agents/skills/README.md) for details.
