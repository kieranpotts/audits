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
reviews, and dynamic testing. After all, security, privacy, and performance
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

Avoid offering fixes or alternative designs. An audit report SHOULD be
evaluation only.

## Prioritize by impact ÷ effort

For each finding, determine:

- **Impact:**
  How much the rest of the codebase will be simplified if the issue is
  fixed. Findings that unlock other improvements rank high.

- **Effort:**
  How invasive the change would be. Local renames rank above cross-cutting
  restructures.

- **Priority:**
  From the impact and effort scores, determine an overall priority rating
  of `HIGH`, `MEDIUM`, or `LOW`. The highest priority items are those that
  will yield the highest impact relative to the effort involved.

Order the findings by priority. The top entry will be the cheapest
high-impact fix.

## Themes

Look for recurring patterns across the findings. You're looking for systemic
issues that individual findings are merely symptoms of. This sort of insight
is often more valuable than any single finding.
