# Draft audit

Prepares a new audit report and opens a draft PR.

## What it does

- Creates an `audit/<slug>` branch from `main`.

- Asks you a few questions and fills out the headers and some initial sections
  of the audit report.

- Writes the draft report to `audits/YYYY-MM-DD-<slug>/README.md`.

- Commits, pushes, and opens a draft pull request titled `audit: <description>`.

## How to invoke

> Draft an audit.

> Draft a new audit report.

> Prepare a new audit report.

> Start an architectural review.

> Prepare an audit of the payment service.

## Recommended models

A fast, inexpensive model is enough. This skill scaffolds files from a
template and fills in metadata — there's no judgment call worth paying for
deeper reasoning.

## Notes

Do the audit and write up the findings yourself. Once there's enough to
review, use [`/review-audit`](../review-audit/README.md) to take the PR out
of draft, then [`/complete-audit`](../complete-audit/README.md) to land it.
