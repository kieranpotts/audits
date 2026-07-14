# Finalize audit

Lands an audit in the `main` trunk.

## What it does

- Confirms review feedback on the pull request has been addressed.

- Squash-merges the pull request with an `audit: <description>` message.

- Deletes the `audit/*` branch.

## How to invoke

From an `audit/*` branch:

> Finalize audit

> This is finalized.

Or specify the target PR:

> Finalize #42

> Finalize the most recent audit.
