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

1.  Create an `audit/<slug>` branch.

2.  Copy the [template](./TEMPLATE.md) to `audits/YYYY-MM-DD-<slug>/README.md`,
    where `YYYY-MM-DD` is the date the architectural audit will be done,
    and where `<slug>` is a short hyphen-delimited description of the
    target software component, subsystem, or service.

3.  Open a draft PR.

4.  Undertake the architectural review.

5.  Write up the report. Add supporting artifacts to the
    `audits/YYYY-MM-DD-<slug>/` directory, referenced from the `README.md`.

6.  Add the audit to index in the `audits/INDEX.md` file.

7.  Open the PR for comments.

8.  Resolve comments and merge into `main`.
