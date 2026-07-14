# Agent skills

Skills available to agents in this repository are:

- **[Scaffold audit](./scaffold-audit/)**:
  Cuts an  `audit/<slug>` branch from `main`, fills in some initial details,
  and opens a draft pull request.

- **[Finalize audit](./finalize-audit/)**:
  Lands an audit in the `main` trunk.

A typical journey runs: scaffold → review via PR → finalize.
