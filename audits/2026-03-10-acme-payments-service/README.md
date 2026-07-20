# Payment service architecture review

> [!NOTE]
> This is a sample audit report, included to illustrate the format. It
> describes a fictional system and does not reflect a real audit.

- **Auditors:** Jane Doe [@janedoe]
- **Audit date:** 2026-03-10
- **Audit PR:** #12
- **Scope:** acme/payments-service@a1b2c3d

## Summary

The payments service is functionally sound but has accumulated structural
debt around its webhook handling. The core checkout flow is well-factored.
The concern is concentrated in one subsystem rather than spread system-wide.

## Scope and method

Examined the `acme/payments-service` repository at the pinned commit, via
static reading and a module-depth walk of the `src/` tree. Dependency
direction was checked with a manual import graph. Test suites and CI
configuration were out-of-scope, as was any cross-reference against the
service's design docs.

## Findings

| ID  | Finding                                                         | Type                  | Priority | Location                          |
| --- | --------------------------------------------------------------- | --------------------- | -------- | --------------------------------- |
| F01 | Retry and idempotency logic tangled into the webhook controller | Tangled dependency    | HIGH     | `src/webhooks/stripe.ts`          |
| F02 | `PaymentGateway` wraps a single caller                          | Single-caller wrapper | LOW      | `src/gateway/PaymentGateway.ts`   |

### F01 — Retry and idempotency logic tangled into the webhook controller

- **Type:** Tangled dependency
- **Priority:** HIGH
- **Location:** `src/webhooks/stripe.ts`

The Stripe webhook handler interleaves three separate concerns in one function:
HTTP request parsing, the exponential-backoff retry loop for downstream calls,
and the idempotency bookkeeping that prevents a redelivered Stripe event from
being processed twice.

Because the retry and idempotency logic lives inline in the transport handler
rather than behind its own seam, it cannot be unit-tested without simulating a
full webhook request, and a change to either the retry policy or the idempotency
check forces a re-read of the whole handler. It also makes the handler the
easiest place for a subtle idempotency bug to hide — directly on the
payment-state path.

### F02 — `PaymentGateway` wraps a single caller

- **Type:** Single-caller wrapper
- **Priority:** LOW
- **Location:** `src/gateway/PaymentGateway.ts`

`PaymentGateway` exists solely to be called from
`src/checkout/CheckoutService.ts`. It adds an indirection layer without
adding behavior beyond what the underlying SDK client already provides,
making the checkout flow one hop harder to trace.

## Themes

Both findings point to the same root cause — payment concerns are not cleanly
separated from the code around them. F01 buries retry and idempotency logic
inside a transport handler; F02 adds an indirection layer that separates nothing.
The service would benefit from clearer seams around the payment-state path.

## Priorities

Resolving F01 would bring the most value, since tangled idempotency logic
directly on the payment path carries real operational risk — a redelivered
Stripe event mishandled here could double-process a payment.
