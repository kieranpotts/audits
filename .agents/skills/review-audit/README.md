# Review audit

Takes an audit report's pull request out of draft once it has enough
substance for review.

## What it does

- Identifies the audit from the current branch (or asks).

- Checks the header metadata is filled in and at least one finding is
  documented.

- Marks the pull request ready for review (`gh pr ready`).

## How to invoke

Run from an `audit/*` branch:

> Review audit

> This audit is ready for review.

Or specify the target PR:

> Review #42

## Notes

This is a light check, not a completeness gate — findings, themes, and
priorities MAY still evolve based on review feedback. Once review is settled,
use [`/complete-audit`](../complete-audit/README.md) to land it.
