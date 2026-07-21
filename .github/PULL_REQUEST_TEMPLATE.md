Briefly describe the audit — the target codebase(s) reviewed and the scope of
the report (the whole system or a specific part of it).

- Audit report: `audits/YYYY-MM-DD-<slug>/README.md` (REQUIRED)
- Target codebase revision, eg. `<team>/<repo>@<commit-hash>`: (RECOMMENDED)

> [!IMPORTANT]
> Use the PR comments for review feedback. The GitHub issue tracker is not
> part of the audit workflow — keep discussion here on the pull request.

----

## Checklist

On opening this PR (open it as a draft):

- [ ] The branch is named `audit/<slug>`.
- [ ] The report is saved at `audits/YYYY-MM-DD-<slug>/README.md`, with the
      metadata header filled in.
- [ ] Supporting artifacts live under `audits/YYYY-MM-DD-<slug>/` and are
      referenced from the report's `README.md`.
- [ ] A row is prepended to `audits/INDEX.md`.
- [ ] The report is written in American English.
- [ ] The report is dated and expressly scoped to the whole system or a
      specific part of it.
- [ ] Every finding cites specific files and lines. Vague findings like
      "the API schema is inconsistent" are removed.
- [ ] Findings are limited to the as-built static structure of the code and
      data. Security/privacy findings and drift-from-design commentary are
      out-of-scope and not included.
- [ ] The report is evaluation only — no suggested fixes, alternative
      designs, or code/PR changes against the audited repositories.

Mark this PR ready for review when:

- [ ] No generic template text or unfilled placeholders remain.
- [ ] The PR title follows `audit: <description>` — a short prose title,
      written full lowercase, eg. `audit: payment service architecture review`.

Merge this PR when:

- [ ] Review feedback is resolved.
- [ ] The PR is set to squash-merge with the commit message `audit: <description>`.

After merging, complete these tasks:

- Delete the `audit/*` branch.

> [!IMPORTANT]
> Audit reports on `main` are immutable snapshots in time, not living
> documentation. Do NOT edit a merged report — file a new audit instead.
