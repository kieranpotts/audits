# Review audit

Checks an audit report has enough substance for review, and takes its pull
request out of draft.

## How to invoke

Run from an `audit/*` branch:

> Review audit

> This audit is ready for review.

Or specify the target PR:

> Review #42

## Recommended models

A fast, cheap model is sufficient for this skill. The completeness check is
deliberately shallow, and the report itself is left untouched.
