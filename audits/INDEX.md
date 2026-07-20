# Audit index

This is a catalog of every audit report merged into `main`.

The index is an append-only stack. Reports are treated as immutable once they
are added to the index.

Audit reports are listed newest first. The date is when the system was examined.

| Date       | Scope                                                                      | Priority findings                                       |
| ---------- | -------------------------------------------------------------------------- | ------------------------------------------------------- |
| 2026-05-22 | [acme/notification-worker@f4e5d6c](./2026-05-22-acme-notification-worker/) | Queue consumer imports template rendering directly      |
| 2026-03-10 | [acme/payments-service@a1b2c3d](./2026-03-10-acme-payments-service/)       | Retry/idempotency logic tangled into webhook controller |
