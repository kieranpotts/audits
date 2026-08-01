# Complete audit

Lands an audit in the `main` trunk.

## What it does

- Confirms review feedback on the pull request has been addressed.

- Confirms the pull request is not still a draft (see
  [`/review-audit`](../review-audit/README.md)).

- Squash-merges the pull request with an `audit: <description>` message.

- Deletes the `audit/*` branch.

## How to invoke

From an `audit/*` branch:

> Complete audit.

> Merge the audit.

> This is completed.

Or specify the target PR:

> Complete #42

> Complete the most recent audit.