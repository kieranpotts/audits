# Best practices

Practical guidance for running a good architecture audit session, and writing
up your report.

## Static structure, not runtime qualities

It is RECOMMENDED that architecture audits be scoped to an evaluation of
the static structure of code and data.

It is best practice for security and privacy reviews to be handled separately,
via specialist threat modeling processes, with findings maintained in a
[risk register](https://github.com/kieranpotts/risks).

Likewise, performance and other runtime qualities are best evaluated through
separate processes — in this case, through dynamic testing.

Inevitably there will be some cross-over between architecture audits, security
reviews, and dynamnic testing. After all, security, privacy, and performance
are core architectural concerns. But by maintaining security audits and
performance tests separately, architecture audits are left to be more narrowly
focused on the long-term static health of a system — its maintainability,
extensibility, portability, auditability, and so on.

## Fresh perspectives

Architecture audits work best when they are blind to the intended design
or to the trade-offs already considered.

A reviewer with no prior context is more likely to surface genuinely novel
problems – smells that crept in silently, or were never considered in the first
place.

It is not always possible to have different people review a system from those
who designed and built it. If this is not possible in your organization, you
can leverage AI tools to offer fresh perspectives on the structural health of
the systems under your stewardship.

## Cite evidence, not impressions

Every finding SHOULD name specific files and lines.

"The API layer is messy" is not an actionable finding. More useful is something
like:

> `handlers/orders.go:120-180` duplicates the same three-step validation
> across five handlers.

## Observation, not solutions

State what you see and the cost it imposes.

Avoid offering fixes or alternative designs. An audit reports SHOULD be
evaluation only.

## Prioritize by impact

Order findings by how much they'd simplify the system and reduce the cost of
its maintenance and future development.

As a general rule, the changes that will have the biggest impact — even if
they are expensive to do — are the ones most worth doing.
