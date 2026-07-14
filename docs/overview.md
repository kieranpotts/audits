# Overview

An audit is a point-in-time evaluation of what a system's architecture actually
is. It is distinct from [design docs](https://github.com/kieranpotts/design),
which are a living description of what the architecture is intended to be
right now.

Audits are scoped to architecture. Security and privacy review should be
handled separately in specialist threat modeling sessions.

## Point-in-time

Design docs, RFCs, and specifications are all kept in lock-step with
production. A change is merged only once the corresponding code is live, so
`main` is always current.

An architecture audit works differently. It is a snapshot, accurate as of the
commit it examined, and immutable once merged to `main`.

The [audit index](../audits/INDEX.md) accumulates a chronological trail of
audits, each dated and scoped, so a reader can see when the system was last
examined, and what was found when.

## Blind to the intended design

An audit evaluates the as-built system on its own terms. It does not consider
the [design docs](https://github.com/kieranpotts/design) or compare
the code against the intended architecture.

The blindness is what makes an audit useful. A reviewer who already knows
the intended architecture, and the trade-offs already considered, tends to
rediscover the same trade-offs. A reviewer with no prior context is more likely
to surface genuinely novel problems – smells that crept in silently, or were
never considered in the first place.

## Structural design

An architecture audit is scoped to the structural design of a system. It looks
for code smells like shallow abstractions, tangled dependencies, single-caller
wrappers, leaky boundaries, and repeated patterns. Findings are fed into
downstream refactoring work.

Security and privacy review is deliberately out of scope. Injection points,
broken authentication or authorization boundaries, unsafe secrets handling, and
similar concerns are not audit findings. They are identified through threat
modeling and tracked in the [risk register](https://github.com/kieranpotts/risks).

Keeping the two apart means each stays sharp. An audit is a fresh structural
read of the code, while the risk register is a living account of security
exposure over time.

If an audit incidentally spots a security concern, the finding should be referred
to the risk register, rather than be recorded in an architecture audit report.
