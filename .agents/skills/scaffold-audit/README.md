# Scaffold audit

Prepares a new audit report and opens a draft PR.

## What it does

- Creates an `audit/<slug>` branch from `main`.

- Asks you a few questions and fills out the headers and some initial sections
  of the audit report.

- Writes the draft report to `audits/YYYY-MM-DD-<slug>/README.md`.

- Commits, pushes, and opens a draft pull request titled `audit: <description>`.

This skill merely scaffolds a new audit report and its PR for review. It
does not assist in evaluating the architecture and writing the final report.
For that, see the [`audit`](https://github.com/kieranpotts/skills/tree/main/skills/audit)
skill in my global agent skills collection.

## How to invoke

> Draft a new audit report.

> Start an architectural review.

> Prepare an audit of the payment service.
