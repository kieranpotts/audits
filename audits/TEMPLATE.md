# Audit title, eg. "Payment service architecture review"

- **Auditors**: Your Name [@your-github-handle], ...
- **Audit date**: YYYY-MM-DD
- **Audit PR**: #...
- **Scope**: owner/repo@<commit>, or the subsystems/services examined

## Summary

A short, single-paragraph verdict on the overall health of the system as-built,
and the headline concerns. What is the shape of the problem?

## Scope and method

What was examined (repositories, services, directories) and how (eg. static
reading, dependency graphing, the deletion test, a module-depth walk).

State what was deliberately out of scope, so the audit's coverage can be judged.

## Findings

The core of the audit. Each finding names a structural problem in the as-is
system, its location, and why it matters. Evaluation only — suggest, do not
prescribe improvements. Order by priority.

Security and privacy concerns are out of scope. Refer any you notice to the
[risk register](https://github.com/kieranpotts/risks) rather than listing them
here.

| ID  | Finding     | Type                  | Priority | Location         |
| --- | ----------- | --------------------- | -------- | ---------------- |
| F01 | Short title | Shallow abstraction   | HIGH     | component / path |
| F02 | Short title | Tangled dependency    | MEDIUM   | component / path |
| F03 | Short title | Single-caller wrapper | LOW      | component / path |

### F01 — Short title

- **Type**: Shallow abstraction | Tangled dependency | Single-caller wrapper |
  Duplication | Leaky boundary | Inverted dependency | Misnamed abstraction | ...

- **Priority**: HIGH | MEDIUM | LOW

- **Location**: The component, module, or path where it lives.

What the problem is — describe the structure that exists. Why it matters —
the cost it imposes (changeability, coupling, comprehension).
Optionally, a suggested way forward — how it might be improved.

### F02 — Short title

- **Type**: ...

- **Priority**: ...

- **Location**: ...

...

## Themes

Recurring patterns across the findings — the systemic issues that individual
findings are symptoms of. Often more valuable than any single finding.

## Recommendations

A prioritized shortlist of what to address first. This list may feed
downstream refactoring and design work.
