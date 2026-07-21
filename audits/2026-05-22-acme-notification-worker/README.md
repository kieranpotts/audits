# Notification worker architecture review

> [!NOTE]
> This is a sample audit report, included to illustrate the format. It
> describes a fictional system and does not reflect a real audit.

- **Auditors:** John Smith [@johnsmith]
- **Audit date:** 2026-05-22
- **Audit PR:** #19
- **Scope:** acme/notification-worker@f4e5d6c

## Summary

The notification worker is a small, single-purpose service in reasonable
shape. One tangled dependency was found between its queue consumer and its
templating layer, which otherwise have no reason to know about each other.

## Scope and method

Examined the `acme/notification-worker` repository at the pinned commit,
via static reading and a manual import graph across `src/`. Infrastructure
and deployment configuration were out-of-scope.

## Findings

| ID  | Finding                                            | Type               | Priority | Location            |
| --- | -------------------------------------------------- | ------------------ | -------- | ------------------- |
| F01 | Queue consumer imports template rendering directly | Tangled dependency | MEDIUM   | `src/consumer.ts`   |

### F01 — Queue consumer imports template rendering directly

- **Type:** Tangled dependency
- **Priority:** MEDIUM
- **Location:** `src/consumer.ts`, `src/templates/render.ts`

`src/consumer.ts`, whose job is to read messages off the queue and dispatch
them, imports `render()` from `src/templates/render.ts` directly and calls
it inline. This couples message dispatch to template rendering, so a change
to either forces a re-read of both, and the consumer cannot be tested
without the templating layer in place.

## Themes

A single finding, so no cross-cutting theme beyond the specific coupling
noted above.

## Priorities

F01 is the only finding, and is a reasonable next fix given its footprint
is limited to two files.
