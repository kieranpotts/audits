# Audits

This directory holds every audit report.

## Structure

```
audits/
├── INDEX.md            # The catalog of merged audits, newest first.
├── TEMPLATE.md         # Template for a new audit report.
└── YYYY-MM-DD-<slug>/  # One report, dated by when the audit was done.
    ├── README.md       # The main entry point to the audit report.
    └── …               # Dependency graphs, exports, or other evidence.
```

## Workflow

1.  An audit is opened as a pull request on an `audit/<slug>` branch, scaffolded
    by the [`draft-audit`](../.agents/skills/draft-audit/) skill.

2.  A report consists of _at least_ a README file, based on the
    [template](./TEMPLATE.md) and saved at `audits/YYYY-MM-DD-<slug>/README.md`,
    covering the architecture findings.

3.  The `INDEX.md` row for the audit is added in the same pull request (unlike
    a numbered catalog, no merge-assigned sequence number is at stake here, so
    there's no need for a separate post-merge commit).

4.  On merge, via the [`land-audit`](../.agents/skills/land-audit/) skill, the
    report and its index row land together.
