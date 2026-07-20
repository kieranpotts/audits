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

| ID  | Finding                                | Type                  | Priority | Location                          |
| --- | -------------------------------------- | --------------------- | -------- | --------------------------------- |
| F01 | Webhook handler duplicates retry logic | Duplication           | HIGH     | `src/webhooks/*.ts`               |
| F02 | `PaymentGateway` wraps a single caller | Single-caller wrapper | LOW      | `src/gateway/PaymentGateway.ts`   |

### F01 — Webhook handler duplicates retry logic

- **Type:** Duplication
- **Priority:** HIGH
- **Location:** `src/webhooks/stripe.ts`, `src/webhooks/paypal.ts`,
  `src/webhooks/adyen.ts`

Each of the three webhook handlers reimplements the same exponential-backoff
retry loop, with small, seemingly accidental variations in the max-retry
count and jitter calculation. This makes it easy for the providers' retry
behavior to drift out-of-sync without anyone noticing, and any fix to the
retry logic has to be applied three times.

### F02 — `PaymentGateway` wraps a single caller

- **Type:** Single-caller wrapper
- **Priority:** LOW
- **Location:** `src/gateway/PaymentGateway.ts`

`PaymentGateway` exists solely to be called from
`src/checkout/CheckoutService.ts`. It adds an indirection layer without
adding behavior beyond what the underlying SDK client already provides,
making the checkout flow one hop harder to trace.

## Themes

Both findings point to the same root cause — logic that should live in one
shared place has been left to be reimplemented per call site.

## Priorities

Resolving F01 would bring the most value, since retry-behavior drift across
payment providers carries real operational risk.
